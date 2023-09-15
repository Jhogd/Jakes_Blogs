---
title: Sorting my head
date: 14-09-2023
---


Today was the last day I had to prepare for a big demo tomorrow. The first demo in which I will be the sole developer so I really want everything to be perfect. I spent most of the day figuring out the best way to display the correct stories in iterations and milestones. I know we want to ALWAYS display a story in the iteration milestone if the stories :iteration attribute or :milestone attribute is set to that respective entity. Now we also want to still maintain the order of stories in their end list if the story is supposed to be there. This was actually more difficult than it originally seemed. There is no easy way to sort the contents of one vector based upon the contents of the other vector without some loop which I desperately wanted to avoid. Luckily I did and it started with using the function map-indexed which maps the index to the value and I did this for the edn list of the current entity. Then I used this function,
```clojure
(-> (map #(when (contains? (set filtered-by-entity) (second %))(second %)) index-map) remove-nil vec)
```
This essentially maps the second number of the index-map which is the actual id if the filtered-by-entity list contains that number therefore maintaining order but getting rid of any numbers that are not supposed to be there.  Next I needed to check if we need to add an id to the end of the that if there is an id in the filtered-by-entity that is not in the new re-ordering. It seems simple now but wow it took me a decent while to realize the correct functions I needed to use. I like these data structure problems because it makes me think outside of the box and I am glad that this is working and all other functionality remains.
