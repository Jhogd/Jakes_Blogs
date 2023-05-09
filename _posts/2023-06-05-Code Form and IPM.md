---
title: Code Form and IPM
date: 06-05-2023
---


Clean Code: Fundamentals, Episode 5

FORM:

Every team should have a coding standard and everyone on the team should follow it. The standard should be seen in the code we shouldn’t
need a separate document giving official rules to the code.

If comments are mandated programmers write them because they have to not because they are useful.

Comments should be rare and used when they are absolutely necessary.

The code itself should express intent and newer languages are perfect for this.

Every comment should be seen as  a failure of the coders ability to express intent without comments but sometimes they are necessary.

If you add a comment make sure to add something new don’t simply restate what the code says.

Don’t add comments that reference code that is far away, if you must add comments make sure its right next to the code it is referencing.


Kill commented out code no ned to keep commented out code!!!!

White space should be treated as importantly as the rest of the code. 

Formatting is about communication and code that communicates well is even more important than the functionality of the code.

Lines should be about 30-40 characters long and we should try to avoid lines that are over 80 characters long
we don’t want the reader to have to scroll to see the full code.


A maximally cohesive method manipulates every variable within the class and a maximally cohesive class contains only maximally cohesive methods.

Use “Tell don’t ask” to avoid writing getters and setters.

When you add a method to a class it ruins independent deployability and all inherited classes need to be re compiled. 

Data structures and switch statements are immune to new functions as you just need to add a new switch statement and it 
does not break independent deployability.

The key to independent deployability is to know what form to use for the given situation. Classes and objects are used when dealing with new types and data structures and switch statements if new methods are added.

An interface is necessary to separate the database from application code.

A database row is actually a data structure and it is not an object. 

The application layer should have a set of interfaces that declare data access methods, we would like our business objects 
to use those interfaces to access the data they need and on the other side of the boundary we would like a set of classes that 
derive from those interfaces and implement the data access methods by grabbing the data structures from the database. 

Views should know about the application but the application should know nothing about the views and these rules of boundaries
are crucial to good software and OOP design. Source code dependencies that cross a boundary should point towards the abstractions 
and away from the concrete side and this is one aspect of a principle called dependency inversion principle.

IPM:


My first IPM happened today and I am looking forward to completing all of my work throughout the week. 
I am getting more comfortable with Clojure as I complete Euler problems and this week I should take an even bigger 
leap by completing my first Kota, giving a presentation on SRP, watching Uncle Bob's videos, and continuing to solve euler problems.
