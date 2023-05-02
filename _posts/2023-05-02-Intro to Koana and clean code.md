---
title: Intro to Koana and clean code
date: 05-02-2023
---
Clean Code: Fundamentals, Episode 2
Names++


Choose your names thoughtfuy- You don’t want to confuse yourself or the reader by having names that are way too simple or overly complicated. The names should have a direct meaning to the piece of code you are writing.
	Avoid silly words like ‘manager’ ‘data’, ‘processor’, ‘info’

Communicate your intent- if you need to add a comment to describe the name it is a bad name.

Avoid disinformation- If you have to read the code to understand what the name means it is also a bad name. 

Pronounceable names - Create names that people can pronounce no need to make overly large or hard to read names.

Avoid encodings- Don’t need to use Hungarian notation don’t need to keep track of types like we used to.

Names should mean what they say and say what they mean.

Booleans should have a name that invokes a question like ‘GreaterThanFive’ as this makes sense to return a true or false.
Classes and variables are nouns or noun phrases such as ‘PointsScored’

Methods are verbs

Enums are typically adjectives like Color, Size, status etc..

Shorter variable names are often a great idea as they are called many times, and writing out a long name over and over again can become gratuitous.

All of these rules make the code read like web written prose and help display the developer cares about their code.


Clean Code: Fundamentals, Episode 1
Clean Code

The Productivity trap:
 
Over time the messiness of the code builds up until things that would have taken days to complete are now taking weeks or months and being productive becomes harder and harder.

 
Managers may give deadlines based on how fast the work was completed in the beginning but not realizing that your productivity is slowing down due to messy code.

 
Brook's Law - If you add more staff to a late project than the project becomes even later and takes longer to complete.
 
 
If you add new employees than they will learn from the people who created the messy code and so the trend continues down while the company is paying even more people so the gap worsens.


 
Don’t want a race between the team that studys the old code and tries to reform it and the team that adds features and works on the current code.
 
 
 
CODE ROT:


Code starts clean but becomes messy as complexity is added.


Rigidity:

system that resists change meaning you have to change a lot of the code to change one thing because parts of the code are dependent on other parts of the code.
 
Fragility:
 
 
System can malfunction in many ways if just a simple change is made or a bug Is fixed, essentially a cascade of broken modules from changing one module
 
Opacity:

Reading the code gives little information as to what it does or the intention of the code.
Code is hard to read hard to change and hard to understand.
 
Developers never go back and clean code after a deadline is complete. Code should be clean from the start. It is worth the time to create clean coherent code because it speeds things up in the long term and short term.
 
What is clean code?
 
 
Clean code is simple and direct and it reads like well written prose.
CleanCode is written by someone who cares.


KOANAS:

Currently working through the beginnning koanas to understand the syntax, methods and data types of clojure.
Tomorow I will finish all of the koanas and the blog willl be about what I learned.
