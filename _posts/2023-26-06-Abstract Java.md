---
title: Interfaces in Java
date: 26-06-2023
---

Say we have a square class with a square constructor that has a width

public class Square implements Shape {
    public int width;
```java
    public Square() {
        System.out.println("Square empty ctor");
    }

    public Square(int width) {
        System.out.println("Square constructor");
        this.width = width;
    }

    public int area() {
        return width * width;
    }
}
```
And we have a circle class with a constructor that has the parameter radius.

public class Circle implements Shape {
    public int radius;
```java
    public Circle(int radius) {
        this.radius = radius;
    }

    public int area() {
        return (int)Math.PI * radius * radius;
    }
}

```
Now we we want to add two shapes to a list and perform the area method upon them. 
```java
@Test
void testAreas() {
    Square s = new Square(5);
    Circle c = new Circle(5);
    List<Object> shapes = new ArrayList<>();
    shapes.add(s);
    shapes.add(c);

    int total = 0;
    for (Object shape : shapes) {
        total += shape.area();
    }
```
Why is this not working? Well area is a method of Square and Circle but we are telling it that each shape within shapes is an Object and Objects do not have the method area().

```java
int total = 0;
for (Object shape : shapes) {
    if(shape instanceof Square)
        total += ((Square) shape).area();
    else if(shape instanceof Circle)
        total += ((Circle) shape).area();
    total += shape.area();
}
```
This would require us to do something complicated and messy like this for us to call area on each shape.

To fix this we will create an abstract shape class or an interface that contains the area method. Circle and Square will implement this shape interface. This allows us to declare that the list made of Shapes
```java
@Test
void testAreas() {
    Square s = new Square(5);
    Circle c = new Circle(5);
    List<Shape> shapes = new ArrayList<>();
    shapes.add(s);
    shapes.add(c);

    int total = 0;
    for (Shape shape : shapes) {
        total += shape.area();
    }
```
Now we are telling the for loop that we are iterating through Shape and pulling one shape form the list shapes at a time. We can also now simply call the area method on each shape because shape is a Shape.
