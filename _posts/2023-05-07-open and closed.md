---
title: open and closed
date: 05-07-2023
---

Though I was able to get the required functionality of my server, it is not configured properly to allow new web applications to run on the server without modifying the server itself to add a new resource path. To change this I am following the command design pattern. Instead of using a switch statement and different cases for each potential resource path and then calling the designated function, I am breaking each functionality into its own class. This way I can utilize what would be similar to a multi method in Clojure by having each class implement a Serve interface that has a sendResponse() function. Now I can have a map of every resource and class and then I can call sendResponse based on the incoming resource or path.

```java
serveMap.get(partialResource).sendResponse(output, resource);
```
