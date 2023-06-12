---
title: Database commands in clojure
date: 09-06-2023
---

For my tic-tac-toe application I was tasked with creating a database that holds data for each game and each move of the game. I had done something similar already with file persistence just simply using text files to save game boards and retrieve them when needed. The logic was basically the same with the database in the sense that I want to be able to resume a game if it was not finished. Java has a really nice library for working with sqlite called jdbc and it allows for some very simple and straightforward database commands. For example, these first four functions below allow me to insert data into my specified database and grab last id’s with very few sql commands.

```clojure
(defn insert-game [game-number difficulty1 difficulty2]
   (jdbc/insert! create-connection
                 :game
                 {:gamenumber game-number
                  :difficulty1 difficulty1
                  :difficulty2 difficulty2}))

(defn grab-last-id-game []
  (get (first (jdbc/query create-connection  ["select id from game order by id desc limit 1"]))
   :id))

(defn grab-last-id-board []
  (get (first (jdbc/query create-connection  ["select id from board order by id desc limit 1"]))
       :id))

(defn insert-board  [board player game-id]
  (jdbc/insert! create-connection
                :board
                {:state (str board)
                 :game_id game-id
                 :player player}))

(defn grab-last-state []
  (let [board-player (jdbc/query create-connection
                                    ["select state, player from board order by id DESC limit 1"])
        game-difficulty1-2 (jdbc/query create-connection
                                  ["select gamenumber, difficulty1, difficulty2 from game order by gamenumber desc limit 1"])
        board (:state (first board-player))
        player (:player (first board-player))
        game-number (:gamenumber (first game-difficulty1-2))
        difficulty1 (:difficulty1 (first game-difficulty1-2))
        difficulty2 (:difficulty2 (first game-difficulty1-2))]
    (->game-state (if (nil? board) board (read-string board)) (if (nil? player) player (read-string player)) game-number difficulty1 difficulty2)))
```


This last function queries both databases and returns the data that will be passed into the core program to resume unfinished games if needed.

