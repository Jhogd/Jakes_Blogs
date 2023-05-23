---
title: Adding difficulty to something that is unbeatable
date: 22-05-2023
---

Adding difficulty to an unbeatable AI:


Today I began working on adding multiple features to my tic-tac-toe game including the 
addition of multiple different play types like human vs human, ai vs ai, a four by four version of 
the game and difficulty settings for the ai. I needed to incorporate an easy setting which would 
mess up often, a medium setting which messes up sometimes and then of course the 
unbeatable ai which I already have implemented. After a decent amount of time and thought about 
how I could get the  ai to mess up I came up with a solution involving random number generators. 
For easy I have  the level currently set to 0.8 and I generate a random number between 0-1. If 
this random  number generated is less than 0.8 than we choose a random empty piece to be our ai move, 
else we select the optimal move. Medium is set up in a similar way but the level is placed at 0.3 

 ```clojure
(defn easy-move [board]
  (let [level 0.8]
    (if (< (rand) level)
      (rand-nth (list-empties board))
      (best-move board))))

(defn medium-move [board]
  (let [level 0.3]
    (if (< (rand) level)
      (rand-nth (list-empties board))
      (best-move board))))

 ```
The code still runs and all I had to do was add a “ask-player-difficulty” function and then add 
that to the main play loop.
I also made slight changes to the ai-turn function, and created a new function called difficulty 
which receives user difficulty level and deviates the ai to run easy, medium or unbeatable.

 ```clojure
(defn difficulty [level board]
  (cond
    (= level "easy") (easy-move board)
    (= level "medium") (medium-move board)
    (= level "unbeatable") (best-move board)
    ))

(defn ai-turn [board difficulty-level]
  (let [ai-move (difficulty difficulty-level board)]
    (println (str "AI has chose move:" ai-move))
    (player-move board X ai-move)))
 ```

So far I am happy with the changes as it has required extremely little modification of my code 
and has mostly been extensions. I also think the way I factored the difficulty settings works well 
and is pretty cool.
