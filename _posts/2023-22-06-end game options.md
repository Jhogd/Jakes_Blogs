---
title: End game options
date: 22-06-2023
---



Part of my menu-options story this week was to have an end game option that would ask the user if they wanted to play again. This initially stumped me because I knew I had to reset the game-map that was passed around to its beginning state. I also did not want to create another draw-button function as I had a two button draw function and a three button draw function. Due to this, I decided to also have a quit button that would close the gui without having to click on the x in the upper corner of the gui. I found a way to do both of these by simply creating another screen option of :game-over and when the user selects the play again button it simply exits the gui and calls the main-sketch again. This is simple enough as quil has a built in function q/exit. I can use this function for quitting the game as well, but there is one small hiccup. After going into the declaration and definition of the function I found that it waits for the next draw to be called before actually exiting the gui so I would have to pass back the game-map or it would throw an error.
```clojure
(defmethod handle-mouse :game-over [game-map coord]
    (cond
      (button-selected? (:x coord) (:y coord) 250 0) (do (q/exit) (main-sketch) game-map)
      (button-selected? (:x coord) (:y coord) 250 100) (do (q/exit) game-map)
      :else
      game-map))

```
My solution is to wrap the play-again in a do function where I exit the gui, call main-sketch again and then also return the game-map. Similarly, for the quit button I call the exit as well as passing the game-map back to the draw function.
