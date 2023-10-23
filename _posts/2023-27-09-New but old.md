---
title: New but old
date: 27-09-2023
---

I’ve come to the middle of the week and a little over halfway done with the iteration. Today I mostly worked on implementing the story modal changes. Most of them are not to hard to implement but it is always challenging to rewrite the tests that exist so that they are accurately testing the new features and changes instead. I don’t want to just delete the old tests and write new ones because I know a lot of the tests that exist are testing things that exist in both the old implementation of the story modal and the new. Now there are obviously times when I just create brand new tests because Im adding some feature like the see more ability on the activity history, but there are lots of tests that just needed rewriting to work for the change like. Examples are changing the acceptance criteria editing buttons, or all of the tag changes. I changed the edit button for the tags, I changed the location of the edit, I changed the buttons to save and cancel a tag edit and creating a tag was slightly changed as well in terms of the placement as well as the logic to open that versus the edit. Since all of my changes still have the same overall functionality of the original todos and the same outcome I could still keep all of the tests because they where well tested before and it would be waste to start from scratch. I guess what I mean is I kept the same functionality of the tests but I had to basically rewrite them so that it would work with the new code I wanted to write. I did the same thing for a lot of the story modal changes because I wanted to make sure I had the same level of testing on the new one as it had for the old modal. So, in good news I have basically completed all of these changes and can move on to finishing the java upgrade and the current members in the project story. 