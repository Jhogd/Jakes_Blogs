---
title: Quacks like a duck
date: 26-05-2023
---

Liskov Substitution principle


The biggest takeaways I have from this principle are:

A subclass can do more but NEVER less than the base class.

Unexpected behaviors like exceptions are bad.

“Is a” is not as clear and straightforward as it appears to be.

Generalizes classes and promotes clean inheritance.

A square should not be inherited from rectangle even though it “is a” rectangle instead they should both be inherited by a shape class.

Limits chance of bugs or any breaks in the system.

Anywhere you call an object of the base class you should be able to replace it with an object of the subclass.
