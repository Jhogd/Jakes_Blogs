---
title: Tic-Tac-Toe beginnings and Euler 7
date: 15-05-2023
---


First Two Weeks


Tic Tac Toe in Clojure and Euler 7




I have begun working on recreating my tic tac toe game using clojure and I have already found 

myself working at a faster pace than I did when I originally created tic tac toe game in python. I 

have created a function to initialize a board and also a function to determine the terminal state 

of the game, a make-move function and I have begun working on win conditions and cpu A.I.



```clojure
(defn init-board []
	  (vec (repeat 9 nil)))

(defn has-empty-space [board]
	(some nil? board))

(defn make-move [board move player]
	(assoc board move payer)
```
I was defining my players like this:
```clojure
(def X \x)
(def O \o)

```
I plan on making the win conditions and terminal states based on the win conditions today as 

well as beginning to make the min max function and best move function for the AI. I hope to 

get over halfway done with the entire program by the end of the day.



I have also competed Euler 7 and I learned something new about a common function.

I have two functions that I started with for checking if a number is prime

```clojure
(defn mod-equal-zero? [dividend divisor]
  (zero? (mod dividend divisor)))

(defn prime-number? [n]
  (if  (= n 1)
    false
    (empty? (filter #(mod-equal-zero? n %) (rest (rest (range n)))))))
```


I needed to find the nth prime number so instead of doing a take while I learned that I can 

create an infinite range with the range function and then lazily take from it with the nth function
```clojure
(defn nth-prime [n]
  (nth (filter prime-number? (range)) n))
```
This way I achieve my desired result and it is done lazily meaning the sequence is computed 

on demand based on the input n

