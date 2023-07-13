---
title: Updates
date: 29-06-2023
---

When attempting to serve the different responses I needed for the http server. I found difficulties when trying to figure out how to get the correct file path and serve that file when the link was a file that actually needed to be loaded instead of a directory. Luckily, java has a couple packages named Files, Path and Paths which provide many useful functions. For example I can call Files.probeContentType to get the mime type of the file path. This can then be used to be displayed in the html header response as Content-Type. The Files class also has a Files.readAllBytes(filePath) which allows me to get the bytes of whatever file I want to send and I can then write those bytes to the output socket. The file class also allowed me to create a file with the current directory and index.html, and I could check to see if this file exists using another built in function to the library. This made searchign for the index.html file and serving it very easy.
