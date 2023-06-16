---
title: Multimethod Dispatching
date: 14-06-2023
---

Today is going to be a shorter blog post but I wanted to share something interesting I came across while working on my tic-tac-toe application. I had been refactoring a lot and turning  redundant and unnecessary code into multi methods to achieve polymorphism and I discovered something new about multi methods. Typically I would use multi methods like this:
```clojure
(defmulti print-board :dimension)

(defmethod print-board :two [board]
  (doseq [row (partition (:size board) (:state board))]
    (println (str/join " | " row))))

(defmethod print-board :three [board]
  (doseq [layer (partition 9 (:state board))]
    (doseq [row (partition (:size board) layer)]
      (println (str/join " | " row)))
    (println (str/join "---" (repeat (:size board) "+")))
    (println)))

```
I am simply dispatching the same function name based on the keyword dimension within the board parameter that is called to the function. I first ran into an issue with this when I tried to do this same thing with more than two parameters in the methods.


```clojure
(defmulti play-game :display)

(defmethod play-game :print [board player game-number difficulty difficulty2]
    (loop [game-board board current-player X]
          (save-current-board game-board current-player game-number difficulty difficulty2)
          (print-board game-board)
          (if (terminal? game-board)
            (game-over game-board current-player game-number difficulty difficulty2)
            (let [new-board (process-game-board game-board current-player player difficulty difficulty2)]
              (recur new-board (switch-player current-player)))
            )))
```

This was throwing a wrong number of arguments to keyword :display. I was puzzled by this for a while because my multi methods with one and two parameters worked just fine when defined in this manner. Eventually I learned that you can only define a multi method to dispatch like this when there is a maximum of two parameters and beyond that you need to do something like this.

```clojure
(defmulti play-game (fn [x & args] (:display x)))
```
I am explicitly telling it that it is a function with multiple arguments and that it needs to dispatch based on the display of the first parameter x.
