---
title: Three-dimensions in two dimensional space 
date: 15-06-2023
---


Representing  a 3d object on a 2d surface can always be a bit challenging and it presented quite the challenge for me when I had to do this for my tic-tac-toe gui. I know quit has the ability to represent three dimensions but I already had a lot to do and it would be simpler to capture the coordinates for playing a move on a two-dimensional space. What I came up with was drawing three operate tic-tac-toe boards with operation between them


```clojure 
(defmulti draw-grid :dimension)

(defmethod draw-grid :two [board]
  (let [square (square-size board)]
    (doseq [x (range 0 (:size board))
            y (range 0 (:size board))]
      (q/stroke 0)
      (q/fill 255)
      (q/rect (* y square) (* x square) square square))))

(defmethod draw-grid :three [board]
  (q/background 255)
  (let [square (square-size board)
        shift (* square (:size board))]
    (doseq [layer (range  3)]
    (doseq [x (range 0 (:size board))
            y (range 0 (:size board))]
      (let [shift-x (* shift layer)]
      (q/stroke 0)
      (q/fill 255)
      (q/rect (+ (* y square) shift-x) (+ (* x square) shift-x) square square))))))
```
I also needed a multi method for drawing X and O
```clojure
(defmulti draw-move :dimension)

(defmethod draw-move :two [board]
  (doseq [x (range 0 (:size board))
          y (range 0 (:size board))]
    (let [square (square-size board)
          half-size (/ square 2)
          player (get-player board (+ x (* y (:size board))))
          color (player-to-color player)]
      (q/stroke 0)
      (q/stroke-weight 2)
      (q/fill color)
      (cond
        (= player :x) (q/text "X" (+ (* x square) half-size) (+ (* y square) half-size))
        (= player :o) (q/text "O" (+ (* x square) half-size) (+ (* y square) half-size))
        :else
        nil))))

(defmethod draw-move :three [board]
    (let [square (square-size board)
          shift (* square (:size board))
          half-size (/ square 2)]
      (doseq [layer (range 0 3)
              x (range 0 (:size board))
              y (range 0 (:size board))]
        (let [shift-x (* shift layer)
              player (get-player board (+ x (* y (:size board)) (* layer (* (:size board) (:size board)))))
              color (player-to-color player)]
          (q/stroke 0)
          (q/stroke-weight 2)
          (q/fill color)
          (cond
            (= player :x) (q/text "X" (+ (* x square) half-size shift-x) (+ (* y square) half-size shift-x))
            (= player :o) (q/text "O" (+ (* x square) half-size shift-x) (+ (* y square) half-size shift-x))
            :else
            nil)))))
```
Final product-

<img width="550" alt="image" src="https://github.com/Jhogd/Jakes_Blogs/assets/132307935/cf2430ff-147c-4892-8b41-854a6fa43967">
