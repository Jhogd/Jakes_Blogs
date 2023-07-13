---
title: Learning more
date: 30-06-2023
---
I have now got my server up and running where every feature is working besides the guessing game. I am happy that I have the directories and other requests set up well but I believe the game will be the hardest one. Something new that I am glad I got to start learning about is html and formatting correct html responses. At first I did not have complete responses and I did not know how to wrap text in a link but through a bit of research I was able to format my html responses correctly. Here is an example of my /hello welcome page

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 7
<html><body><h1>Welcome!</h1></body></html>

Links happen to be pretty simple as well.
```java
listing.append("<li><a target='_blank' href='").append(file.getPath()).
                append("'>").append(file.getName()).append("</a></li>");
```
