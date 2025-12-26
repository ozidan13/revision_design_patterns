# SET412 Factory Design Pattern
---

## Agenda

*   Definition
*   Advantages
*   Implementation
*   Abstract Factory.

---

## Definition

*   The Factory Method is a creational design pattern that defines an interface for creating objects but lets subclasses decide which object to instantiate.
*   It promotes loose coupling by delegating object creation to a method, making the system more flexible and extensible.
    *   Subclasses override the factory method to produce specific object types.
    *   Supports easy addition of new product types without modifying existing code.
    *   Enhances maintainability and adaptability at runtime.

---

## Problem

*[Illustration: A complex logistics scene. On the left, a winding road with trucks transporting goods. In the center, a logistics facility with crates and cranes. On the right, a river with boats transporting goods. The scene represents a mix of road and sea logistics.]*

---

## Problem

*[Illustration: A diagram showing a central "LogisticsApp". This app is tightly connected via tangled lines to multiple specific "Truck" instances. On the right, a confused character is holding a "Ship" object, wondering how to fit it into this tangled network of truck dependencies.]*

---

## Solution

**UML Diagram Description:**

*   **Abstract Creator (Class: Logistics)**
    *   Methods:
        *   `+ planDelivery()`
        *   `+ createTransport()` (Abstract Factory Method)
        *   *(Note: `planDelivery` calls `createTransport` internally: `Transport t = createTransport()`)*

*   **Concrete Creators (Subclasses of Logistics)**
    1.  **RoadLogistics**
        *   Method: `+ createTransport()`
        *   Implementation: `return new Truck()`
    2.  **SeaLogistics**
        *   Method: `+ createTransport()`
        *   Implementation: `return new Ship()`

*   **Relationship:** Both `RoadLogistics` and `SeaLogistics` inherit from `Logistics`.

---

## Solution

*[Illustration: A revised architecture diagram. The "LogisticsApp" is now central. It connects to a "Transport" abstraction. The specific "RoadLogistics" creates "Truck" instances that conform to "Transport". The "SeaLogistics" creates "Ship" instances that conform to "Transport". The lines are organized, indicating a decoupled structure where the app works with the "Transport" interface rather than specific classes.]*

---

## Components

*   **Product:**
    *   Abstract interface or class for objects created by the factory.
*   **Concrete Product:**
    *   The actual object that implements the product interface.
*   **Creator:**
    *   Declares the factory method.
*   **Concrete Creator (Concrete Factory):**
    *   Implements the factory method to create specific products.

---

## Structure

**UML Diagram Description:**

1.  **Creator (Abstract Class/Interface)**
    *   Methods:
        *   `+ someOperation()`
        *   `+ createProduct(): Product` (Abstract)
    *   Note: `Product p = createProduct()` is used inside `someOperation`.

2.  **ConcreteCreatorA (Extends Creator)**
    *   Method: `+ createProduct(): Product`
    *   Implementation: `return new ConcreteProductA()`

3.  **ConcreteCreatorB (Extends Creator)**
    *   Method: `+ createProduct(): Product`
    *   Implementation: `return new ConcreteProductA()` *(Note: Diagram text says `+ createProduct(): Product`)*

4.  **Product (Interface)**
    *   `«interface» Product`
    *   Method: `+ doStuff()`

5.  **ConcreteProductA** and **ConcreteProductB**
    *   Both implement the `Product` interface.

---

## Class Diagram

**Diagram Description:**

*   **Shape** (`<<Interface>>`)
    *   Method: `+draw() : void`
*   **Concrete Shapes** (Implement `Shape`):
    *   `Circle`: `+draw() : void`
    *   `Square`: `+draw() : void`
    *   `Rectangle`: `+draw() : void`
*   **FactoryPatternDemo**
    *   Method: `+main() : void`
    *   Action: Asks `ShapeFactory`
*   **ShapeFactory**
    *   Method: `+getShape() : Shape`
    *   Action: Creates `Circle`, `Square`, or `Rectangle`.

---

## Implementation: Step 1

*   Create a(n) Product / interface.

```java
public interface Shape {
    void draw();
}
```

---

## Implementation: Step 2

*   Create concrete classes implementing the same interface.

```java
public class Triangle implements Shape {

    @Override
    public void draw() {
        System.out.println("Draw Triangle");
    }

}
```

---

## Implementation: Step 2

*   Create concrete classes implementing the same interface.

```java
public class Rectangle implements Shape {

    @Override
    public void draw() {
        System.out.println("Draw Rectangle");
    }

}
```

---

## Implementation: Step 2

*   Create concrete classes implementing the same interface.

```java
public class Circle implements Shape {

    @Override
    public void draw() {
        System.out.println("Draw Circle");
    }

}
```

---

## Implementation: Step 3

*   Create a Factory to generate object of concrete class based on given information.

```java
public class ShapeFactory {
    public Shape getShape(String shapeType){
        if(shapeType == null){
            return null;}
        if(shapeType.equalsIgnoreCase("Circle")){
            return new Circle();
        } else if(shapeType.equalsIgnoreCase("Rectangle")){
            return new Rectangle();
        } else if(shapeType.equalsIgnoreCase("Triangle")){
            return new Triangle();
        }
        return null;
    }
}
```

---

## Usage of Factory Pattern

*   MAIN METHOD

```java
public static void main(String[] args) {
    ShapeFactory shapeFactory = new ShapeFactory();
    Shape shape1 = shapeFactory.getShape("CIRCLE");
    Shape shape2 = shapeFactory.getShape("RECTANGLE");
    Shape shape3 = shapeFactory.getShape("Triangle");
}
```

---

## Advanatges

*   Avoid tight coupling between the creator and the concrete products.
*   Single Responsibility Principle.
    *   Move product creation code into one place in the program
    *   Allow for easier code support.
*   Open/Closed Principle.
    *   Present new types of products into the program without breaking existing client code.