---
title: Rendering on the fly
date: 06-10-2023
---


Today is Thursday and I am feeling pretty good going into the demo tomorrow but I still had to complete a couple stories. For one, I implemented some new changes Olive made to the labels so that just one shows up when you create a project rather than 10. Another change was some buttons, she removed a cancel button when you edit an existing label so instead if you tab or lose focus of the input it saves the whatever you had written, and I kept the cancel button for creating a new label but it can also save on-blur. The more complicated story I had to finish was fixing performance issues on the site. I wanted to only render stories for an iteration when ti comes in view. I spent about 4 hours making a complicated set of functions to adjust a render count based on ratios of view size and offset and incrementing based on how far you have scrolled. This was very complicated and error prone. Instead after a tiny break I realized that I can get the size of an iteration div and simply calculate how many iterations are in view by adding the view offset which is what we can see and the scroll offset. When I add them together I have the render size and I can simply divide this number by the size of each iteration to get the new render number. This worked as I expected and was about 50 less lines of code. It was very satisfying to reduce the amount of code I was writing by such a large amount and that is also worked better. 
```clojure
(defn determine-render-count []
  (let [total-iterations   (total-iterations @state/project)
        scroll-container   "#-execute-view #-story-bar-scroll-container"
        node               (dom/select scroll-container)
        offset             (dom/scroll-left node)
        view-size          (dom/width-by-id "-execute-view")
        iteration-size     (dom/client-width (str scroll-container " .-story-bar-list-item"))
        visible-iterations (Math/ceil (/ (+ offset view-size 1) iteration-size))]
    (reset! render-iteration-count (update-render-count visible-iterations total-iterations))))
```
This the main function I used and the update-render count simple checked if the visible number was greater than the total iterations in the project and if it was I return the total rather than the visible.
