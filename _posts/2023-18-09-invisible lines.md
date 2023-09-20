---
title: Invisible lines
date: 18-09-2023
---

Today I began my week by completing the welcome new user flash message that should appear when a user is entering their project for the first time. This story was not too difficult to complete but I did have to make some slight changes to the memberc file. We already had a last-entered-at attribute that was used for sorting the project list in the users home page so I knew I could use this attribute to help with the story. Originally when new member is create they are given a last-entered-at time of the current time. I decided to make this value null when the user is created and so now I can place a check in the ws-enter-project function that checks to see if they have a last-entered-at value. If they do then we display no message, if not display the welcome sign. I think it makes more sense for the attribute to set up this way anyways as they are not always entering a project immediately after having a membership created and so now it only gets attached when they actually enter the project. Next I worked on displaying the correct amount of empty lines or white space in the acceptance criteria of the story modal. After a bunch of testing I found that the issue actually lied with the markup to hiccup function as it would seemingly get rid of the additional /n’s in the text when converting the text. To get around this I made a function that checks the description for white space and replaces it with <p> which acts as a empty line when it goes through markdown. Tomorrow I will be working on implementing the rest of the story modal changes and its my birthday woooooooo!