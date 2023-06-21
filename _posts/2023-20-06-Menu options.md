---
title: Whats on the Menu?
date: 20-06-2023
---

This week I have been tasked with adding menu options to the gui of my tic tac toe application.

Last week I had created the gui so that it could run the games but it still prompted for user 

input in the terminal. I knew this would require buttons that the user could select that would 

move them to the next screen of options and build upon the starting map with all of the user 

specifications. To do this I decided to make draw and update-gui multi methods that could 

dispatch based on the current stage in the selection stage.
```clojure
(defmulti update-gui :screen)

(defmethod update-gui :persistence [game-map]
  game-map)

(defmethod update-gui :new-old [game-map]
  game-map)

(defmethod update-gui :game-mode [game-map]
  (if (contains? (:board game-map) :age)
    game-map
    (update-in game-map [:board] conj {:age :new})))

(defmethod update-gui :ask-difficulty [game-map]
  game-map)

(defmulti draw :screen)

(defmethod draw :game [game-map]
  (q/clear)
  (draw-grid (:board game-map))
  (draw-move (:board game-map))
  )

(defmethod draw :persistence [game-map]
  (q/clear)
  (let [text1 "Data-base"
        text2 "Edn-file"]
    (draw-two-button-menu text1 text2)))

(defmethod draw :new-old [game-map]
  (q/clear)
  (let [text1 "Resume"
        text2 "New-game"]
    (draw-two-button-menu text1 text2)))


(defmethod draw :game-mode [game-map]
  (q/clear)
  (let [text1 "ai-vs-human"
        text2 "human-vs-human"
        text3 "ai-vs-ai"]
    (draw-three-button-menu text1 text2 text3)))

(defmethod draw :ask-difficulty [game-map]
  (q/clear)
  (let [text1 "easy"
        text2 "medium"
        text3 "unbeatable"]
    (draw-three-button-menu text1 text2 text3)))

```
This is not all of the  variations of draw and update but this is how I was able to keep it so that 

the main sketch only needed to call “draw” and “update-gui” and it can pass around the map 

as it updates and switches screens. I then have a function that calculates if the user selected a 

button which prompts the map to update.
