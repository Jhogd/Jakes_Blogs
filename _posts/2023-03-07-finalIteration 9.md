---
title: final for Iteration 9
date: 03-07-2023
---

I am very happy to say that I have completed my initial HTTP server. This was a very challenging task and it forced me to learn a lot of new topics and apply that learning to code in just a week. I am definitely happy I got to do this project because it showed me how much more I still need to learn especially when it comes to building servers and websites. A very useful tool I found when trying to figure out how to build the guessing game was a concurrent hash map. With this map I was able to store the gameId with the random number associated with that id. So, in the case that multiple people are running the game, they will all have different random numbers they are trying to guess and my server will keep track of what random number belongs to who.
```java
public static int initGameResponse() throws IOException {
        int randomNumber  = (int) ((Math.random() * 100) +1);
        int gameId = randomMap.size();
        randomMap.put(gameId, randomNumber);
        return gameId;
    }
```
