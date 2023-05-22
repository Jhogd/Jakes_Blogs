---
title: Polymorphism
date: 19-05-2023
---

Polymorphism

Polymorphism as used in object oriented programming allows objects to respond to the same 

method call based on their specific implementation and have different results. An example is 

having an area class that can handle different types of shapes like squares, triangles and 

circles and all of these shapes will have slightly different area methods but they are all shapes 

and they all have an area. Polymorphism is typically done through inheritance where there is a 

class and a subclass that is inherited from the base class. Both the class and subclass can 

have a method with the same name but the subclass’s ,ethos can override the base class 

method to provide a specialized implementation. A square and triangle can both derive from a 

shape class where an area method is defined but both the square and triangle can have 

specialized area methods that account for the difference between the types. Polymorphism 

can also typically be achieved through interfaces where the interfaces define a set of methods 

that the implementing classes must implement. Multiple classes can implement the same 

interface and objects of all the classes can be treated the same allowing the code to operate 

on general interfaces and not dependent on specific implementations. Generally,  

polymorphism enables developers to write code that can work with objects of multiple types 

providing flexibility, reusability and extensibility. 


Polymorphism in clojure:

Polymorphism in clojure can be achieved in multiple ways and one of those is by using 

defprotocol and defrecord. 

```clojure
(defprotocol Shape
  (area [shape])
  (perimeter [shape])
  )

(defrecord Rectangle [width height]
  Shape
  (area [shape]
    (* (:width shape) (:height shape)))
  (perimeter [shape]
    (* 2 (+ (:width shape) (:height shape)))))

(defrecord Circle [radius]
  Shape
  (area [shape]
    (* 3.14 (:radius shape) (:radius shape)))
  (perimeter [shape]
    (* 3.14 (:radius shape))))

(def circle (->Circle 7))
(def rectangle (->Rectangle 7 5))

(defn -main [& args]
  (println (area circle))
  (println (perimeter rectangle))
  )
```
Here I am able to create a shape protocol that houses two functions, area and perimeter. These 

functions can then be implemented within different records like circle and rectangle and they 

can have variations to how thy are implemented for each record.

As I have detailed in previous blog posts multi methods and methods can also be used to 

achieve polymorphism. Outside of those two is another way of achieving polymorphism which 

is through definterface which allow us to create interfaces within clojure.
