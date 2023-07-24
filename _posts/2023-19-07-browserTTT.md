---
title: How I did it 
date: 19-07-2023
---

Learning how to use reagent and write clojurescript was a bit of a challenge but I am happy that I eventually got everything to work. The foundation of my code is built on a reagent atom that contains the same map I use for all other versions of the game making it simple to get the users specifications and play the game. 
```clojure
(defonce game-map (r/atom (conj (utility/->game-state nil nil 0 nil nil) {:playing? false})))
```
I also added a playing? Boolean which will determine if the menu or the game is to be displayed. Next I define the different menu questions such as what type of board the user wants to play on. This is done using radio buttons that update the current game map atom using an on-change event. This means whenever a button is clicked or pressed it will update the map. 
```clojure
(defn select-board-menu []
  [:p [:strong "Select a Board: "
       [:br]
       [:br]
       [:label "3 by 3"]
       (input-field "board" (conj (utility/init-board (utility/->Three-by-three)) {:display :gui})
                    #(update-map :board (conj (utility/init-board (utility/->Three-by-three)) {:display :gui})))
       [:br]
       [:label "4 by 4"]
       (input-field "board" (conj (utility/init-board (utility/->Four-by-four)) {:display :gui})
                    #(update-map :board (conj (utility/init-board (utility/->Four-by-four)) {:display :gui})))
       ]])
```
Next, I create the table using a create-square function which is a button that has a on-click event which calls either a human-turn or an ai turn function depending on whos turn it is. This create-square function is called in a create-row function which calls the square either three or four times depending on the size. Finnaly, the create row function is called in a create-table function which again calls create-row three or four times. The rest of the code is simply specifying what to do when a new game is started and a function that acts as a main to create a game.
```clojure
(defmethod create-square true [current-game-map position]
    (doall
    [:td
     [:button {:id  position :style  {:color "blue"
                                      :font-size "30px"
                                      :display "inline-block"
                                      :background-color "black"
                                      :padding "50px 50px"}
               :on-click #(update-game-state (play-human-turn (:board current-game-map) (:player current-game-map)
                                                              position))}
      (key-to-string (nth (:state (:board @game-map)) position))]]))
```
