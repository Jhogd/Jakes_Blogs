---
title: Array-list and Linked-node implementation
date: 08-06-2023
---



Last week I wrote a blog post going over the differences between array-lists and linked-nodes and this week I have correctly implemented those in Clojure. In this blog post I will show examples of how I implemented them and their associated functions


Array-lists

```clojure
(defn create-array-list []
  (let [data  (atom (make-array Integer/TYPE 10))
        size  (atom 0)]
    {:kind :array :data data :size size}))
```
We start by creating a java array of base size 10 using an atom for the data
```clojure
(defn ensure-capacity [arr-list]
  (let [data (:data arr-list)
        current-size (count @data)]
    (when (= @(:size arr-list) current-size)
      (swap! data #(into-array  (concat % (make-array Integer/TYPE current-size)))))))
```
If we run out of space and want toads then we need to create more space
```clojure
(defn array-get [arr index]
  (if (zero? index)
    (first arr)
    (recur (rest arr) (dec index))))
```
A function to retrieve a value from the array with an index
```clojure
(defmethod add :array [arr-list element]
  (let [data (:data arr-list)
        size (:size arr-list)]
    (ensure-capacity arr-list)
    (aset @data @size element)
    (swap! (:size arr-list) inc)
    arr-list))
```
Add value to array-list
```clojure
(defmethod get :array [arr-list index]
  (let [data (:data arr-list)
        size (:size arr-list)]
    (if (and (integer? index) (>= index 0) (< index @size))
      (array-get (vec @data) index)
      (throw (Exception. "Index out of bounds”)))))
```
Function to get a value from an array-list with an index
```clojure
(defn array-set [arr index value]
  (if (zero? index)
    (conj (rest arr) value)
    (assoc arr index value)))

(defmethod remove :array [arr-list index]
  (let [data (:data arr-list)
        size (:size arr-list)]
    (if (and (integer? index) (>= index 0) (< index @size))
      (do
        (dotimes [i (- @size (inc index))]
          (array-set (vec @data) (+ index i) (array-get (vec @data) (+ (inc index) i))))
        (swap! (:size arr-list) dec)
        (array-set (vec @data) @size nil))
      (throw (Exception. "Index out of bounds”)))))
```
Removing a value given an index 
```clojure
(defmethod size :array [arr-list]
  @(:size arr-list))
```

Linked-node

```clojure
(defn create-linked-list []
  (atom {:kind :linked-list :head nil}))
```
Creating a base linked-list
```clojure
(defn create-node [data]
  (atom {:data data :next nil}))
```
Creating a node
```clojure
(defn last-node [list]
  ;(prn " list: "  list)
  (loop [current (:head list)]
   ; (prn "current: " current)
    (if (nil? (:next @current))
      current
      (recur (:next @current)))))
```
Retrieves the last node from the linked-node
```clojure
(defn add-list [list data]
  (let [new-node (create-node data)]
    (if (nil? (:head @list))
      (swap! list assoc-in [:head] new-node)
      (let [last-node (last-node @list)]
        (swap! last-node assoc-in [:next] new-node)))))
```

Adds a new node to the end of the linked-node
```clojure
(defn get-list [list index]
    (loop [i 0
           current (:head @list)]
      (if (= i index)
        (:data @current)
        (recur (inc i) (:next @current)))))
```
Gets a value given an index
```clojure
(defn size-list [list]
    (loop [count 0 node (:head @list)]
      (if (nil? node)
        count
        (recur (inc count) (:next @node)))))
```
Retrieves the size of the linked-node
```clojure
(defn remove-list [list index]
  (if (nil? (:head @list))
    list
    (let [size (size-list list)]
      (if (or (>= index size) (<= index -1))
        list
        (let [values (vec (for [i (range size)
                                :when (not= i index)]
                            (get-list list i)))]
          (swap! list @(create-linked-list))
            (prn "list" list)
          (doseq [value values]
            (add-list list value))
          )))))
```
Removing a node given an index
```clojure
(defn display-list [list]
  (loop [current (:head @list)]
  (if (nil? current)
    nil
    (do
      (print (:data @current) "->")
      (recur (:next @current))))))
```
Displaying all the values stored in the linked node.


The hardest part of implementing these data structures was that I had to use atoms to hold state because by nature maps and most data structures in Clojure are immutable and so I could not do things like calling the add function multiple times in a. Row and achieving the desired affect because it would simply replace the current value instead of adding to it like it needs to. I am happy I did this though because I learned a lot about how to use atoms correctly.
