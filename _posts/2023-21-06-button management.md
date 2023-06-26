---
title: Handling the mouse
date: 21-06-2023
---

The creation of buttons in quil was something that initially stumped me and I was going about in the wrong 

way. Initially I just had a function such as handle-mouse that would check if the mouse was clicked and then 

perform logic based on the coordinates. This did not work as as there was nothing within the main sketch call 

that called a mouse-click function, instead I had placed it within the main game loop when it was the 

humans turn. This is wrong for a variety of reasons, one quil passes around a map and continuously calls the 

functions defined in the sketch which means it would keep calling the draw and update without caring about 

my mouse-click. Additionally, the q/mouse-clicked? function was not being used properly. To fix this 

We must define a mouse-clicked function in the sketch
```clojure
(defn main-sketch []
  (q/sketch
    :title "Tic-Tac-Toe"
    :host :host
    :middleware [m/fun-mode]
    :size [300 300]
    :setup setup
    :draw draw
    :mouse-clicked handle-mouse
    :update update-gui
    ))
 ```
Now mouse-clicked calls handle-mouse on every iteration the gui runs. 
```clojure
defmethod handle-mouse :game [{:keys [screen board current-player player game-number difficulty difficulty2] :as state} coord]
  (if (human-turn? board current-player player)
    (let [move (mouse-to-board board (:x coord) (:y coord))]
      (if (is-empty? (:state board) move)
        (let [new-board (player-move board current-player move)]
          (save-current-board new-board (switch-player current-player) game-number difficulty difficulty2)
          {:screen screen :board  new-board :current-player (switch-player current-player)
           :player player :game-number game-number :difficulty difficulty :difficulty2 difficulty2})
        state))
    state))
```
Now it will call handle-mouse all the time but it will simply return the map if it is not the humans-turn.

In other cases of menu options I had to think about what clicking a button is and that is simply when the mouse coordinates are within your button or box
```clojure
(defn button-selected? [x y y-offset y-offset2]
  (and (and (> x (- (q/width) 220)) (< x (+ (- (q/width) 220) (/ (q/width) 2))))
       (and (> y (+ (- (q/height) y-offset) y-offset2)) (< y (+ (+ (- (q/height) y-offset) y-offset2) (/ (q/height) 5))))))
```
This button function is called in all of the handle-mouse methods for the menu options and we 

just simply check if it was clicked based on the inputed coordinates.
