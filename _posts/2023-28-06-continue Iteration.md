---
title: Iteration Continued
date: 28-06-2023
---

While progressing through my server program, I reached a point where I needed to start testing that the information I am writing to the output stream is correct and that it is properly writing to it. I assumed the testing for this would be difficult that maybe I would need to make a mock output stream. It turns out it is very simple because you can call .toString on your output. All you need to do is create a new output stream, call your function and then convert your output in the test to a string. Now you can compare this output string to any expected string that you might want your output stream to receive.
