---
title: Better together
date: 10-07-2023
---

The ability to use Java and Clojure interchangeably in the same project is one of the numerous benefits that Clojure Ofers and its an important skill to know. I think one of the biggest questions I had going into this project was how I was going to implement an interface I had created in my java HttpServer. Turns out it was way simpler than I would have imagined, in fact most of the trouble I found when combining a Clojure and java project was how to call and implement java methods in Clojure. Implementing the interface is as simple as creating a deftype and then having it implement the java interface. You can then create your own version of the interface method like this.
```clojure
(deftype ServeTTT []
  Serve
  (sendResponse [this out resource]
    (cond
      (= resource "/ttt") (serve-menu out)
      (str/includes? resource "ttt?") (serve-initial-game out resource)
      :else (serve-tic-tac-toe out resource)
      )))
```
To call this new implementation of sendResponse that is created under the type Serve you only need to require the namespace that contains this method and then call a new instance of this Serve type like the example below where helper is the namespace ServeTTT exists in.
```clojure
(helper/->ServeTTT)
```
