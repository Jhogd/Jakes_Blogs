---
title: Persistence is Key   
date: 02-06-2023
---

File Persistence using EDN:

I am still new to file persistence, saving states and maintaining a database like structure but 
having to implement an elementary version of this has helped me a lot. Creating a good database
or file keeping system is extremely important to larger real life systems, where tons of data is 
being stored and manipulated. In this case it is only for a simple tic-tac-toe application but 
it still teaches the basics and acts as a good starting point. For my system I created a 
file-persistence file that housed important functions for saving game-states to the base 
file, and grabbing the last board as well as grabbing the entire files worth of games.

```clojure
(defn grab-last-game [file-name]
  (with-open [reader (io/reader file-name)]
    (->> (line-seq reader)
         (remove str/blank?)
         last
         read-string)))

(defn save-board [board current-player game-number level level-two file-name]
  (spit file-name (utility/->game-state board current-player game-number level level-two)
        :append true)
  (spit file-name "\n" :append true))

(defn grab-games [file-name]
  (slurp file-name))
```
 These three functions are the primary handler of the file persistence system. 

```clojure
(def game-state {:board nil :player nil :game-number 0 :difficulty nil :difficulty2 nil})

(defn ->game-state [board current-player game-number level level-two]
   (assoc game-state :board board :player current-player :game-number game-number :difficulty level
```

The game-state map and game-state function work with the save-board function to save the 
board, current player, game-number and two difficulties for the ai’s. Storing all of this provides 
the necessary information to determine if the last game played was finished or not and return 
the required pieces such as the current-player and game-mode so that the user can decide if 
they want to resume their previous game or start a new one. Next I will add a sql database to 
the application and the data will be saved in both the database and the text-file.
