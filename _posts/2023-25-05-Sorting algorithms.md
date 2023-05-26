---
title: Sorting algorithms
date: 25-05-2023
---

Sorting algorithms:


Bubble sort-

The bubble sort is the simplest but perhaps longest and most time consuming sorting 

algorithm that iterates through a collection value buy value comparing it with the next value 

and determining if it needs to be moved or not. Bubble sorting is of time complexity O(N^2) as 

it requires looping over the the collection as each value needs to be compared with the rest to 

make sure it is in the correct spot.

![image](https://github.com/Jhogd/Jakes_Blogs/assets/132307935/aec30284-2ab8-444e-9de0-bfc73c85a483)


Merge-sort-

Merge sort is a much more efficient sorting method than bubble sort especially when it comes 

to very large data structures. The algorithm works by breaking a given collection into a left and 

right side based on the mid point. It then calls itself on the left and right side recursively until 

they cannot be divided any further and then the collections are merged back together and 

sorted one at a time until it is one sorted collection again. The time complexity analysis of this 

algorithm is O(Nlog(N)) making it one of the most efficient sorting methods.


![image](https://github.com/Jhogd/Jakes_Blogs/assets/132307935/b07b85f6-020e-4b54-a42d-0a2febb3a24e)



Quick sort-

I found quick sort to be a very fascinating and effective sorting method that makes a lot of 

sense and is pretty straight forward to implement. The method works by selecting a pivot 

variable then moving every element in the collection either to the left of it if it is smaller than the 

pivot or to the right of the pivot if it is larger. The function calls itself again as a partition from 

where the the initial pivot ended up and then the new pivot is either in the middle, first or last 

element of the new partitioned collections that are called recursively. The collection containing 

the lower elements of the pivot are called as well as the collection of larger elements than the 

pivot. 


<img width="528" length="600" alt="image" src="https://github.com/Jhogd/Jakes_Blogs/assets/132307935/c308880e-cf76-4a4f-af2c-e128f0d34bd8">


The worst case time complexity analysis for this algorithm is O(N^2) when the first or last 

element of a collection is chosen as a pivot and if the collection is already sorted in ascending 

or decreasing order. However, it is O(Nlog(N)) when the middle element is selected as the pivot 

and the collection is not already sorted in any way, so this means the average case is also 

O(Nlog(N)).  
