---
title: Function Structure and Good Practices
date: 05-05-2023
---

Clean Code Fundamentals Episode 4: Function Structure
   
Notes:

Switch statements ruin the independent deployability and develop-ability of a program and they lead to fan-out problems.


Persistent fads in software.


	-Functional programming 

	-Structural programming 

	-Object Oriented Programming


A true mathematical function is dependent only on its inputs

Temporal coupling is when one function must be called before another and the program is dependent on order of function calls.

We can resolve by passing a block where we combine the linked functions so that it always calls the functions in the correct order.


It is a good habit to write your error handling code before your production code.

Functions should not handle error exceptions and do something it should do one or the other.

Function signatures should be small and have few arguments maybe three or fewer. 

We should never pass booleans or nulls into functions and no output arguments!! 

Organize methods according to step down principle where we have public methods at the top and then the methods below them that are called by them and so on. 

We don’t want any backwards references.

Switch statements can be very harmful and they interfere with independent deployability and independent development, 
we should replace them with polymorphism where possible or at least move them down into safe independent deployable modules like main. 

Tell don’t ask describes that the user should handle the problem should tell other objects to do the work, and 
not simply “asking them” don’t ask the objects state and then make the decision should simply tell the objects what to do.



Function side-effects are when a function relies on or modifies something outside its parameters to do something.
