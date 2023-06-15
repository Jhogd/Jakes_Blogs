---
title: Satisfying Refactoring.
date: 13-06-2023
---

I am going to show you something quite horrifying…….
```clojure
(defmulti play-game :game-type)

(defmethod play-game :ai-vs-human [board player game-number difficulty difficulty2]
  (loop [game-board board current-player X]
    (insert-board game-board current-player game-number)
    (save-board game-board current-player game-number difficulty difficulty2 edn-file)
  (print-board game-board)
   (if (terminal? game-board)
      (game-over game-board)
      (if (= current-player player)
        (let [new-board (human-turn game-board current-player)]
          (recur new-board (switch-player current-player)))
        (let [new-board (ai-turn game-board difficulty current-player)]
          (recur new-board (switch-player current-player)))))))

(defmethod play-game :ai-vs-ai [board player game-number difficulty difficulty2]
  (loop [game-board board current-player player]
    (insert-board game-board current-player game-number)
    (save-board game-board current-player game-number difficulty difficulty2 edn-file)
    (print-board game-board)
    (if (terminal? game-board)
      (game-over game-board)
      (if (= current-player X)
        (let [new-board (ai-turn game-board difficulty current-player)]
          (recur new-board (switch-player current-player)))
        (let [new-board (ai-turn game-board difficulty2 current-player)]
          (recur new-board (switch-player current-player)))))))

(defmethod play-game :human-vs-human [board player game-number difficulty difficulty2]
  (loop [game-board board current-player player]
    (insert-board game-board current-player game-number)
    (save-board game-board current-player game-number difficulty difficulty2 edn-file)
    (print-board game-board)
   (if (terminal? game-board)
      (game-over game-board)
      (let [new-board (human-turn game-board current-player)]
        (recur new-board (switch-player current-player)))
      )))

```

Ew…. So, here we have a multi method for each game-type and as you can clearly see this is a lot of redundant and excess code. Not to mention they are all long functions as well which just makes this uglier. Luckily I noticed the pattern and after doing some other refacotrings in my code I was able to turn that mess above into this.

```clojure
(defn play-game [board player game-number difficulty difficulty2]
    (loop [game-board board current-player X count 0]
      (if (progress-game? count (counter-select game-board))
        {:board game-board :player  current-player :game-number game-number
         :difficulty difficulty :difficulty2 difficulty2}
        (do
          (save-current-board game-board current-player game-number difficulty difficulty2)
          (display-game game-board)
          (if (terminal? game-board)
            (game-over game-board current-player game-number difficulty difficulty2)
            (let [new-board (process-game-board game-board current-player player difficulty difficulty2)]
              (recur new-board (switch-player current-player) (inc count)))
            )))))
```
I now have a single function that can handle all game modes because of this multi method 
```clojure
(defmulti process-game-board (fn [x & args] (:game-type x)))

(defmethod process-game-board :ai-vs-human [game-board current-player player difficulty difficulty2]
  (if (= current-player player)
    (human-turn game-board current-player)
    (ai-turn game-board difficulty current-player)))

(defmethod process-game-board :ai-vs-ai [game-board current-player player difficulty difficulty2]
  (if (= current-player player)
    (ai-turn game-board difficulty current-player)
    (ai-turn game-board difficulty2 current-player)))

(defmethod process-game-board :human-vs-human [game-board current-player player difficulty difficulty1]
  (human-turn game-board current-player))
```
I will likely keep factoring and reducing this function but this looks infinitely better than the three large functions I had before.
