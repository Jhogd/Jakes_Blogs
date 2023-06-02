---
title: Multimethod usage
date: 01-06-2023
---


As I worked on refactoring my tic-tac-toe board and added new functionalities and I began to 

better understand how to get the best use out of multi methods in Clojure. They are great for 

achieving polymorphism and getting rid of unsustainable and fragile conditional statements 

and if statements. In my code I needed to add a separate win conditions function for my 3D tic 

tac toe board as the previous one only worked for different sized two dimensional boards. I 

could just create a new differently named function and then create conditionals in my code 

wherever I called the win condition function to dictate if I needed to call the 3D or 2D variation. 

This sounds like a massive headache and will cause my to have to change a lot of my code to 

comply with this new functionality, not to mention it breaks the open closed- principle. Instead I 

created a multi method for a win? function and it dispatches based on the dimension of the 

board

```clojure
(defmulti win? :dimension)

(defmethod win? :two [board player]
  (let [size (:size board)
        rows (partition size (:state board))
        cols (apply mapv vector rows)
        diag1 (for [i (range size)] (nth (nth rows i) i))
        diag2 (for [i (range size)] (nth (nth rows i) (- size (inc i))))
        all-spaces (concat rows cols [diag1 diag2])
        win-cond (fn [space] (every? #(= player %) space))]
    (boolean (some win-cond all-spaces))))

(defmethod win? :three [board player]
  (let [size (:size board)
        rows (partition size (:state board))
        cols (for [i [[0 3 6] [1 4 7] [2 5 8] [9 12 15] [10 13 16] [11 14 17]
                      [18 21 24] [19 22 25] [20 23 26]]]
               (mapv #(get (:state board) %) i))
        diags (for [i [[0 4 8] [2 4 6] [9 13 17] [12 13 15] [18 22 26] [20 22 24]]]
                (mapv #(get (:state board) %) i))
        depth-cols (apply mapv vector (partition 9 (:state board)))
        depth-rows (for [i [[0 10 20] [3 13 23] [6 16 26]]] (mapv #(get (:state board) %) i))
        depth-diags (for [i [[0 13 26] [2 13 24]]] (mapv #(get (:state board) %) i))
        all-spaces (concat rows cols diags depth-cols depth-rows depth-diags)
        win-cond (fn [space] (every? #(= player %) space))]
    (boolean (some win-cond all-spaces))))
```
Now I don’t have to change any of my code that calls the function as it still takes just two parameters and I don’t even have to pass the dimension around the code.
```clojure
(defrecord Three-dimension []
  Board
  (init-board [this] {:state (vec (repeat (* 3 3 3) EMPTY)) :size 3 :dimension :three})
  )
```

This implementation of initializing the board gives the board a :dimension in which the win multi 

method can dispatch appropriately without having to pass in any other variables besides the 

board and player.
