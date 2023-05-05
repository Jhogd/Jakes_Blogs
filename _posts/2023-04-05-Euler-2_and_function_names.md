---
title: Fibonacci Sequence in Clojure and Function Names
date: 04-05-2023
---


Euler # 2 Fibonacci Sequence:


The problem statement was simple. 


Generate a fibonacci sequence beginning with [1 2] and sum they even numbers.



I began problem solving by creating a simple test that would pass if I it was equal to [1 2].



This clearly does not do much but it was a starting point.


I then broke down the problem and wrote a test case for a function that would get the second last element from a sequence. I created a simple function that would do this and then created a test case for a function that would sum the last and second to last element from a sequence. I ended with these two functions

 


    (defn second-last [n]


        (second (reverse n)))
        

    (defn sum-second-last [n]


        (+ (second-last n) (last n)))

                                                                       

After this is when I began to run into problems. I created a test that would test a fib-sequence function when it had an input of 3 meaning the fib sequence would contain a total of 3 values [1 2 3]. 
I began to write a function for this but ran into a stoping point because I was still thinking of the problem from a loop and conditional style of coding attributed to other languages. I found I could generate a fib sequence using the loop and recur functions in Clojure and it looked like this 

    (defn fb-sequence [n]

        (loop [fibs [1 2]]

          (if (= n (count fibs))

            fibs


            (recur (conj fibs (sum-second-last fibs)))))



This style of coding made the most sense to me as I am assigning fibs to initially equal [1 2] and then stating that if the length of fibs is equal to n then we should stop looping, if not then call the function again but conjoin fibs with the sum of the second to last and last value. I then created another test that would test for 5 values so [1 2 3 5 8]. This passed but before I moved on to summing the even values it was suggested to me by Alex that the code could be refactored to look more like clean code written in Clojure.  I wrote a test case that would check if the sum of even numbers in the sequence was correct and then began to re write the function.



The final refactored version of the function looked like this. I also had to rework the function to run until the last value in the sequence was greater than the given input.




    (defn euler-2 [n]
    
    
      (->> (take-while #(< (last %) n) (iterate #(conj % (sum-second-last %)) [1 2]))
      
      
           (last)
           
           
           (filter even?)
           
           
           (apply +)))



I really appreciate how clean this looks and its very easy for a reader to understand what is going on.  We first state that while the last value is less than n we iterate beginning with [1 2] and each iteration we conjoin the result of the sum-second-last with the  current sequence. This generates a list of lists essentially so we take the last list, filter it for even values and then sum it.





Uncle Bob’s rules of functions

———————————————————————

#1 Functions are small

#2 Functions are even smaller than small

#3 They will act like sign posts helping everyone navigate through my code

#4 Functions do one thing 

#5 To ensure a function is doing one thing “extract to you drop”

#6 If you can extract another function from a function then you SHOULD! 

#7 Function names should be directly correlated to what it does

#8 Long function names that help direct the reader are good





