---
title: Beginnings of Clojure
date: 03-05-2023
---


Today I completed the Clojure koans. 


The biggest lesson I learned is that being able to read and understand a language is a lot different than writing it. As I progressed through the koans I began to understand how to read the language and fill in the blanks to make the code pass the tests. This is a good step towards my journey of becoming a clean coder using Clojure but I was immediately humbled when  asked to write my own code and test cases with Micah. I found myself knowing the logical way to solve the problem which in this case was to simply return a list of values less than a given number that are also multiples of 3 and 5. In python I would have ran a for loop that goes over the range from 0-n and applied each number to a function that tests if that number is a multiple of 3 or 5.



Something like this:
```python
  (valid_multiples = [] 
      for x in range(n):
        check_multiple = multipleof_3_or_5(n)
        If check_multiple:
          valid_multiples.append(x)
      final_sum = sum(valid_multiples))
```


This would work in python but Clojure is still very new to me and so I had trouble thinking of a good solution on the spot. I do like Clojure so far and I think it will easily become my favorite language once I practice enough with it. I am just still in the beginning phases of learning to write but practicing everyday will lead to good results.



Now here is the overall code in Clojure that takes an input number and calculates the sum of every number within the range of the input number that is a multiple of 3 and 5.


  ```clojure
   (defn multiple-of-5-3? [n]  
    (or (zero? (mod n 3))
        (zero? (mod n 5))))


    (defn multiples-less-than [n]
      (filter multiple-of-5-3? (rest (range n))))

    (defn euler-1 [n]
      (apply + (multiples-less-than n)))
```
The filter function is extremely useful, it creates a lazy sequence given a function and a list. In this case it is applying the multiple-of-3-5 function to every value in range of n besides the first one which is zero hence the ‘rest’ statement. The filter will only place a value in it’s lazy sequence if it passes true on the function. The next function is straight forward but it uses the apply syntax which applies the first function ‘+’ to the second function it is given ‘multiples-less-than’ using n as the input to the second function. 



The most important thing about solving this problem was using TTD as this is key to becoming a clean coder and I will follow the guidelines set by Uncle Bob rigorously. 

I am excited to keep learning this language and using Test Driven Development to write clean and impactful code.

