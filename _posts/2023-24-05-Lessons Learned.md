---
title: Lessons Ive learned and increasing speed
date: 24-05-2023
---

Working on adding new implementations to this tic-tac-toe game has helped me realize why in 

first hand experience why the SOLID principles are so important. There where multiple 

functions I had to end up changing when requirements changed and it made me realize that I 

did not have the open closed principle in mind when I initially built some of these functions. For 

example, I needed to change my initialize board function to include a size option that will 

create the board for a given N X N like 4 by 4 or 3 by 3. Because of this change I needed to 

update the code wherever I had called the initialize board function, I also had to change my win 

conditions to include size and generalize the winning approach to work for any tic-tac-toe size. 

These changes caused a bit of unnecessary work as I had to go through my code and update 

it everywhere that relied on these functions. Next time I am tasked with a project I need to 

really try and keep in mind potential changes and leave my code open for extension rather than 

modification. The good news is the majority of my code did not need changed and adding all 

the required changes in this weeks story did not cause any major breaks in my code and I was 

able to add options without editing most of the code. The last thing I need to improve on for 

this week is increasing the speed of my algorithm as a 4 by 4 tic tac toe game has 

exponentially more possible moves and therefore a much larger decision tree that needs to be 

computed in order to make the optimal move. The techniques I have implemented are 

memoization and I added a condition in my terminal? Function that checks first to see if 

enough moves have been made for a win before actually checking the win conditions which 

helps speed up the process. With these two things the time as decreased but it is still not fast 

enough so tomorrow I will add alpha beta pruning and try a transposition table. I hope with all 

of these changes my algorithm will be nearly instantaneous.
