# SET412 Abstract Factory Design Pattern


---

## Agenda

*   Intent
*   Problem
*   Solution
*   Structure
*   Methodology
*   Advantages

---

## Intent

*   Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.
*   Use the Abstract Factory when your code needs to work with various families of related products.
*   Abstract Factory provide an interface for creating objects from each class of the product family.
*   As long as your code creates objects via this interface, you don’t have to worry about creating the wrong variant of a product which doesn’t match the products already created by your app.

---

## Problem

*   Imagine that you’re creating a furniture shop simulator. Your code consists of classes that represent:
*   A family of related products, say:
    *   Chair
    *   Sofa
    *   Coffee Table.
*   Several variants of this family.
    *   Modern,
    *   Victorian,
    *   ArtDeco.

---

## Problem (Visual Matrix)

| | Chair | Sofa | Coffee Table |
| :--- | :---: | :---: | :---: |
| **Art Deco** | [Illustration of Art Deco Chair] | [Illustration of Art Deco Sofa] | [Illustration of Art Deco Coffee Table] |
| **Victorian** | [Illustration of Victorian Chair] | [Illustration of Victorian Sofa] | [Illustration of Victorian Coffee Table] |
| **Modern** | [Illustration of Modern Chair] | [Illustration of Modern Sofa] | [Illustration of Modern Coffee Table] |

---

## Solution

*   Abstract Factory pattern suggests is to explicitly declare interfaces for each distinct product of the product family
    *   chair,
    *   sofa
    *   coffee table.
*   Implement variants of products follow those interfaces.
    *   all chair variants can implement the Chair interface;
    *   all coffee table variants can implement the CoffeeTable interface;
    *   So on.

---

## Solution (Diagram)

**Diagram: Class Hierarchy for Chair Product**

*   **Parent:**
    *   `«interface»`
    *   **Chair**
    *   `+ hasLegs()`
    *   `+ sitOn()`

*   **Children (implementing Chair):**
    1.  **VictorianChair**
        *   [Illustration of Victorian Chair]
        *   `+ hasLegs`
    2.  **ArtDecoChair**
        *   [Illustration of Art Deco Chair]
        *   `+ hasOnn`
    3.  **ModernChair**
        *   [Illustration of Modern Chair]
        *   `+ sitOn()`

---

## Solution

*   Declare the Abstract Factory—an interface with a list of creation methods for all products that are part of the product family
    *   CreateChair, createSofa and createCoffeeTable.
*   These methods must return abstract product types represented by interfaces we extracted previously:
    *   Chair, Sofa, CoffeeTable and so on.

---

## Structure

**UML Diagram Description:**

1.  **Abstract Products:**
    *   `AbstractProductA` (Interface)
    *   `AbstractProductB` (Interface)

2.  **Concrete Products:**
    *   `ConcreteProductA1` and `ConcreteProductA2` implement `AbstractProductA`.
    *   `ConcreteProductB1` and `ConcreteProductB2` implement `AbstractProductB`.

3.  **Abstract Factory:**
    *   `«interface» AbstractFactory`
    *   Methods:
        *   `+ createProductA(): ProductA`
        *   `+ createProductB(): ProductB`

4.  **Concrete Factories:**
    *   **ConcreteFactory1** (implements `AbstractFactory`)
        *   `+ createProductA(): ProductA` (Returns `ConcreteProductA1`)
        *   `+ createProductB(): ProductB` (Returns `ConcreteProductB1`)
    *   **ConcreteFactory2** (implements `AbstractFactory`)
        *   `+ createProductA(): ProductA` (Returns `ConcreteProductA2`)
        *   `+ createProductB(): ProductB` (Returns `return new ConcreteProductB2()`)

5.  **Client:**
    *   `Client`
    *   Fields: `- factory: AbstractFactory`
    *   Methods:
        *   `+ Client(f: AbstractFactory)`
        *   `+ someOperation()`
    *   Usage Example: `ProductA pa = factory.createProductA()`

---

## Methodology

*   Map out a matrix of distinct product types versus variants of these products.
*   Declare abstract product interfaces for all product types.
*   Make all concrete product classes implement these interfaces.
*   Declare the abstract factory interface
    *   Include set of creation methods for all abstract products.
*   Implement a set of concrete factory classes, one for each product variant.
*   Create factory initialization code somewhere in the app.
    *   Pass this factory object to all classes that construct products.
*   Replace direct calls to product constructors with calls to the appropriate method on the factory object.

---

## Product - Chair

*   Declare abstract product interfaces for all product types.

```java
package com.setecu.lec04.ex1.interfaces;

public interface Chair {
    void hasLegs();
    void sitOn();
}
```

---

## Product - CoffeeTable

*   Declare abstract product interfaces for all product types.

```java
package com.setecu.lec04.ex1.interfaces;

public interface CoffeeTable {
    void placeItems();
}
```

---

## Product - Sofa

*   Declare abstract product interfaces for all product types.

```java
package com.setecu.lec04.ex1.interfaces;

public interface Sofa {
    void lieOn();
}
```

---

## Concrete product

*   Make all concrete product classes implement interfaces
    *   `public class VictorianSofa implements Sofa.`
    *   `public class VictorianCoffeeTable implements CoffeeTable`
    *   `public class VictorianChair implements Chair`
    *   `public class ModernSofa implements Sofa`
    *   `public class ModernCoffeeTable implements CoffeeTable`
    *   `public class ModernChair implements Chair`
    *   `public class ArtDecoSofa implements Sofa`
    *   `public class ArtDecoCoffeeTable implements CoffeeTable`
    *   `public class ArtDecoChair implements Chair`

---

## Abstract factory

```java
public interface FurnitureFactory {
    Chair createChair();
    Sofa createSofa();
    CoffeeTable createCoffeeTable();
}
```

---

## Concrete Factory Classes

*   Create concrete factory classes.
    *   `public class VictorianFurnitureFactory implements FurnitureFactory`
    *   `public class ModernFurnitureFactory implements FurnitureFactory`
    *   `public class ArtDecoFurnitureFactory implements FurnitureFactory`

---

## Create factory initialization

```java
private static FurnitureFactory factory;

switch (style.toLowerCase()) {
    case "modern":
        factory = new ModernFurnitureFactory();
        break;
    case "victorian":
        factory = new VictorianFurnitureFactory();
        break;
    case "artdeco":
        factory = new ArtDecoFurnitureFactory();
        break;
}
```

---

## Advantages

*   You can be sure that the products you’re getting from a factory are compatible with each other.
*   You avoid tight coupling between concrete products and client code.
*   Single Responsibility Principle.
    *   You can extract the product creation code into one place, making the code easier to support.
*   Open/Closed Principle.
    *   You can introduce new variants of products without breaking existing client code.