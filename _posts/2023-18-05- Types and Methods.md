---
title: Types and methods
date: 18-05-2023
---


Up until recently where I was working on coding examples for my Open-Closed Principle I had 

not worked or looked into types and multimethods in clojure. The vast majority of code I have 

done whether that was for Euler, fizzbuzz kata or the unbeatable tic tac toe game has been with 

standard functions. Types and multi methods appear to be a great way to actively prepare for 

changing requirements and future added functionalities to code. They can be used to instantiate 

different types such as square, circle, triangle and then creating methods for each that have slight 

variation in how we would want to process each of those shapes. A multi method class called area can 

be created and then the methods for each shape are based on this multi method. This allows us to follow 

the open-closed principle because the existing functions for each shape are never modified 

and instead the code is open to modification because new shapes can be added with slight 

variations to their area function without touching existing functions.

For my presentation I created an example based on totaling the cost for a shopping cart where 

each potential item can be defined as its own method within the calculate-total multi method. 

Doing this allows me to add new items with different prices without ever touching a function 

called calculate-total-cost. If the code was not written like this then I would have to actively 

change the calculate-total-cost function as I added new items that the customer could order 

such as shirt, hat book etc…



```clojure
(deftype Book [quantity])
(deftype Shirt [quantity])
(deftype Hat [quantity])

(defmulti calculate-cost class)
(defmethod calculate-cost Book [quantity]
  (* (.quantity quantity) 10))

(defmethod calculate-cost Shirt [quantity]
  (* (.quantity quantity) 15))

(defmethod calculate-cost Hat [quantity]
  (* (.quantity quantity) 5))

(defn calculate-total-cost [cart]
  (reduce
    (fn [total item]
    (+ total (calculate-cost item)))
    0 cart))

(def cart [(Book. 3)
            (Shirt. 6)
            (Hat. 2)])

(defn -main
  [& args]
  (println (calculate-total-cost cart)))

```



Now the code is set up with future requirement changes in mind and I can add new types 

without ever modifying existing code.


The open-closed principle can certainly be applied with regular functions in clojure as well, I 

just liked how clear and straight forward this example is when demonstrating how to make 

code open for extension and closed for modification.
 
