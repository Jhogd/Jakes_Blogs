---
title: Multiple games for Web App
date: 14-07-2023
---

After completing the post request story I needed to also make web app tic-tac-toe stateless in the sense that any number of users can play separate games without interfering with the others game. To do this I had to create a new database function in my original game that will pull the game board and state for a given game ID. This function gets the last entry in the database associated with the specified game number. 
```clojure
(defn current-game-pieces [gameId]
  (let [board-player (jdbc/query create-connection
                                 ["select state, player from board where game_id = ? order by id DESC limit 1" gameId])
        game-difficulty1-2 (jdbc/query create-connection
                                       ["select gamenumber, difficulty1, difficulty2 from game where gamenumber = ? order by id DESC limit 1" gameId])
        board (:state (first board-player))
        player (:player (first board-player))
        game-number (:gamenumber (first game-difficulty1-2))
        difficulty1 (:difficulty1 (first game-difficulty1-2))
        difficulty2 (:difficulty2 (first game-difficulty1-2))   
 (->game-state (if (nil? board) board (read-string board)) (if (nil? player) player (read-string player)) game-number difficulty1 difficulty2)))
```
Now I simply create a hidden input in the html that gets passed the gameID so that we canker track of what game it is.
```clojure
[:input#gameID {:type "hidden" :name "gameID" :value gameID}]]
```
Lastly, I create a function that parses out the gameID from the post body.
```clojure
(defn get-current-game-id [body]
  (let [first-index (+ (str/index-of body "ID=") 3)
        id (subs body first-index)]
    (read-string id)))
```
