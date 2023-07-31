---
title: Doing too much
date: 25-07-2023
---


A common problem that Alex and I seemed to run into while working on Epic was over engineering or over complicating a task. There have been multiple instances of us having to start over after essentially trying to do too much. I wanted to sort the projects for each user by the most recently accessed. My original thought was to add a projects to the User schema. This would begin as an empty string and when a User enters a story, I would see if a project already exists and if it did I would remove it then add that story to the front of the list. This would effectively keep track of the most recently entered projects and we could just get the projects from the User shcema. This is problematic because there is already a method for keeping track of user projects which is the member system. It then becomes an issue of where to pull projects from and it is unnecessary to create another method for keeping track of projects. It is excess code and an over complication of what needed to be done. Instead I added a last-entered-on key to the member shcema and all we have to do to keep track of recent projects is to update and transact that key when a user enters the project. There are more examples we have come across but I am learning to not over engineer problems that don’t need it.
