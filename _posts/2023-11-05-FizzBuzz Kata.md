---
title: FizzBuzz Kata
date: 11-05-2023
---

Performing Fizzbuzz Kata


The fizz buzz kata is a fairly simple beginner kata where the task is to print fizz buzz up to a given number. 

The rules are simple:

If the input is a multiple of 3 we print “fizz”
If the input is a multiple of 5 we print “buzz”
If the input is a multiple of 15 we print “fizzbuzz”

The real test of performing a kata like this is practicing the methodologies of test driven 

development. I have deleted and re wrote this kata ten times this week to really help get myself 

in the habit of TTD. Iteratively developing code has many benefits but I have really been 

amazed at how simple solutions can be derived through this process that I would not have 

came up with without writing tests and taking one small step at a time. I can clearly see the 

benefit of this when developing much larger and complex code because it actually decreases 

the amount of time spent on a project while also reducing headaches. I think this also helps 

avoid getting stuck while coding because you are iteratively doing small problems instead of 

overthinking the larger solution. 


Example of starting the fizzbuzz kata:

We want to find the the simplest possible test case to begin the kata so we will start by simply 

stating this: 
```clojure
(should= 1 (fizz-buzz 1))
```
From here I will create a function that simply returns 1:
```clojure
(Defn fizz-buzz [n]
1)
```
This will pass the test and then we move on to the second simplest test case like this:
```clojure
(should= 2 (fizz-buzz 2))
```
Now I update the function:
```clojure
(Defn fizz-buzz [n]
n) 
```
This will just return the input, Now we get a little more complicated and say this:
```clojure
(should= “fizz” (fizz-buzz 3))
```
I will update the function like this:
```clojure
(Defn fizz-buzz [n]
(If (= 3 n) “fizz” n))
```
This will now return fizz for an input of 3 but return the input in all other cases.


I will then follow these same procedures for the rest of the kata.
