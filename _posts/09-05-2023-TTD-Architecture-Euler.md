---
title: TTD-Architecture-Euler
date: 09-05-2023
---

Test Driven Development:


Test driven development is faster than traditionally written code while also having less defects and being cleaner. 

Rules-
	Never write production code without first having a failing test.
	Write only enough of a test to demonstrate a failure 
	Write only enough production code to pass the failing test

Test driven development eliminates the fear of change that holds programmers back by having tests we can trust with out lives.

Test driven development can often lead to faster and quicker solutions than originally designed 

Guidelines when using TTD:
Write the simple failing test
Write production code so that it passes the simple test.
Refactor if possible


Architecture, Use Cases and High Level Design:

By focusing the architecture by its use cases we can defer decisions about the ui database or other components.
This deferral allows us to keep our options open as long as possible which allows changes to be made without undo cost.
Creates separation  between system components which allows business to make decisions about each of them individually.


When we look at something like an accounting website we should notice that it is an accounting system not a web system even tho it is both a web system and accounting system. The business logic should be what’s apparent and the web system is simply a way to deliver the accounting logic.

When the architecture is based on the use case we see the true intent of the system.

Essentially we want our architecture to contain components that can be deferred which makes the system open to changes and additions but also allows simple and fast TTD for each component. The Use Case should be at the forefront of the architecture 


Euler problems:


I have now completed Euler problems 1-6.
This has helped me learn a lot of the fundamentals of Clojure and test driven development. I can clearly see how writing tests first and taking an interactive and almost naive approach can lead to great results. While developing multiple solutions I found myself coming to a faster and more simple solution than I originally thought when I started the process of solving the problem. I had a very similar experience to an experience Uncle Bob described with the Bowling Kata in which he had originally designed a complex architecture containing classes and sub classes but ended up with a for loop and two iff statements.

Here are some of the important things I learned while completing Euler 1-6

1) Anonymous functions- Can be used to apply a value from a collection that you are iterating through like with this example where I am checking if the last value of the sequence I am generating is smaller than n and I am also using an anonymous function to conjoin the established sequence with the sum of the last two value in the sequence each iteration. The ‘#’ initiates the anonymous function and % is used to represent the anonymous value

```clojure
(defn euler-2 [n]
  (->> (take-while #(< (last %) n) (iterate #(conj % (sum-second-last %)) [1 2]))
       (last)
       (filter even?)
       (apply +)))
```
2) The use of loops is different any Clojure than most languages but I have a solid understanding of how they work now and I have even used a combination of two recursive functions to solve problem 3. Here the mod-loop function is a loop itself which recursively divides a number by another until it is no longer evenly divisible and returns it.
```clojure
(defn euler-3 [n]
  (loop [div n
         fact 2]
    (if (<= div 1)
      (- fact 1)
      (recur (mod-loop div fact) (+ fact 1))))
 ```
3) I got to work with strings in problem 3 and created a very simple function to check palindromes
```clojure
(defn is-palindrome? [potential-pal]
  (= potential-pal (apply str (reverse potential-pal))))
```
4) I know maps are a very powerful tool in Clojure and I am just scratching the surface but I used them to help solve problem 5. In the first function I utilize map and an anonymous function to return a collection of exponential powers based on the largest num and a collection n. The second function is very simple just maps a collection based on the pow function and two collections.
```clojure
(defn exponent-coll [n largest-num]
  (map #(smallest-exponent % largest-num) n))

(defn applied-exponents [prime-collection exponent-collection]
  (map pow prime-collection exponent-collection))
```
I of course learned more than this but these are just a few examples and I am happy that TTD is becoming more natural to me.


