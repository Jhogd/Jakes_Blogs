---
title: OCP and Finishing Tic-Tac-Toe
date: 17-05-2023
---

Open close Principle and Finishing Tic-Tac-Toe



At its core the Open-Closed-Principle advocates designing software in a way that allows for 

easy extensions without requiring modifications to the existing code. The principle emphasizes 

the need to build systems that can evolve and accommodate new features and requirements 

without the risk of introducing new bugs or breaking existing functionality. Code should be 

written from the beginning with the Open-Closed-Principle in mind. There are two major parts 

to the principle and those are “Open for extension” and “Closed for modification”. The first part 

“Open for extension” encourages developers to design their code in a way that new 

functionalities can be implemented without altering already existing code and this can be 

achieved through inheritance, composition or interfaces. The “Closed for modification” aspect 

details that once a module for class is implemented and tested it should remain stable and 

shouldn’t be modified to add new features. Instead, existing functionality should be 

encapsulated so that it is self-contained and isolated from future changes. 

The Open-Closed Principle has many benefits when applied to code:


1)Improved code maintainability

2)Enhanced code reusability

3)Facilitates agile development, faster iteration cycles and better adaptability to to changing requirements

4)Encourages modular design where systems are broke down into smaller more cohesive modules or classes




Finishing Tic-Tac-Toe in Clojure.



By completing this project I have been able to learn a lot of useful and important techniques that will serve me well as I continue my career.

```clojure
(let [moves (atom (range 10))
          next-move (fn [& _] (let [move (first @moves)]
                              (swap! moves rest)
                              move))]
      (with-redefs [best-move next-move
                    read next-move]
        (should= nil (play-game))))))

(defn play-game []
  (loop [board (init-board) current-player X]
    (print-board board)
    (if (terminal? board)
      (cond
        (= (terminal-state board) 1) (println "Ai has won the game")
        (= (terminal-state board) -1) (println "Human player has won the game")
        (= (terminal-state board) 0) (println "The game has ended in draw")
        )
      (if (= current-player X)
        (let [new-board (ai-turn board)]
          (recur new-board (switch-player current-player)))
        (let [new-board (human-turn board)]
          (recur new-board (switch-player current-player)))))))

```

I was initially having trouble finding a way to test my main play loop function as within the 

function I had a function that asked for player movement as well as an AI function that chose a 

best move to play and inserted that move into the game board. I was not going to be able to 

write a simple test like (should= (function input)) because the AI player and human player would 

have varying inputs and outputs. I asked help from Micah and he showed me the testing code 

above that uses (with-redefs) to force certain functions to give static values that allow for 

testing a varying function like my play-game function. Here the best-move  and read functions 

are set to always be equal to the next move which is provided in the code above which simply 

states that the “next-move” is equal to the first value in a range of 0-8 and then that range is 

swapped for 1-8 and then 2-8, 3-8 etc.. With this test I am able to simulate an entire tic-tac-toe

game being played allowing me to see that my play-game function is working as expected and is calling

everything it needsin the correct order to simulate the game. This is a very powerful testing method

that allows complex simulation of functions. 



