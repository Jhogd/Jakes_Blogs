---
title: Continuing Tic-Tac-Toe and Euler 8
date: 16-05-2023
---

I have nearly completed my tic-tac-toe game in Clojure, just need to finish and optimize the 

minimax algorithm and complete my main game play loop. I have had fun recreating this game 

because I can see the distinct differences between how I approached the problem in python 

with no TDD vs in Clojure and writing tests every step of the way. 


Here are some of the functions I have made/updated today.

```clojure

(defn list-empties [board]
  (vec (keep-indexed (fn [index value]
                       (when (= value :e) index)) board)))

(defn win? [board maximize]
  (or (every? #(= maximize %) (subvec board 0 3))
      (every? #(= maximize %) (subvec board 3 6))
      (every? #(= maximize %) (subvec board 5 8))
      (every? #(= maximize %) (mapv #(nth board %) [0 3 6]))
      (every? #(= maximize %) (mapv #(nth board %) [1 4 7]))
      (every? #(= maximize %) (mapv #(nth board %) [2 5 8]))
      (every? #(= maximize %) (mapv #(nth board %) [0 4 8]))
      (every? #(= maximize %) (mapv #(nth board %) [2 4 6]))
      ))

 defn terminal-state [board]
  (cond
    (win? board X) 1
    (win? board O) -1
    :else
      0))

(defn terminal? [board]
(or (win? board X) (win? board O) (not (has-empty-space? board))))


(defn ai-turn [board]
  (let [ai-move (best-move board)]
    (println (str "AI has chose move:" ai-move))
    (player-move board ai-move X)))

(defn human-turn [board]
  (let [move (read)]
    (player-move board move O)))

(defn print-board [board]
  (doseq [row (partition 3 (board))]
    (println (clojure.string/join " | " row))))
    
 ```


These functions have been tested and are good to go I simply need to implement the algorithm and the main play loop.



I also completed Euler 8 today and learned some cool things while doing it.

```clojure
(defn digit-seq [n]
  (if (zero? n)
    []
    (lazy-seq (conj (digit-seq (quot n 10)) (mod n 10)))))

```

This function is generating a vector of digits given an integer, so If the input is 4567 it will return 
[7 6 5 4]. Clearly the reverse is a slight issue but I easily took care of that with the next function

```clojure
(defn sequence-by-13 [n]

    (reverse (map reverse (partition 13 1 (digit-seq n)))))

```
generating This function is creating a vector of vectors using the one above and reversing the order while also partitioning each sequence to contain 13 values. So if the input is 12349234981123 the answer will be 

[[1 2 3 4 9 2 3 4 9 8 1 1 2]
          [2 3 4 9 2 3 4 9 8 1 1 2 3]]

```clojure
(defn euler-8 [n]
  (let [seqs (sequence-by-13 n)
        prods (map #(reduce * %) seqs)]
    (if (seq seqs)
      (apply max prods))))
```
The last function here takes in a large number, assigns seqs to the result of the function above, and prods to the result of reducing each vector within seqs.
Lastly, I make sure seqs is a full sequence and apply the max function to get the largest product.
