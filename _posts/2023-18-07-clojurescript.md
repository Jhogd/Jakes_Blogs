---
title: Beginning clojurescipt
date: 18-07-2023
---

This week I had to create a standalone web page in clojurescript. When I did estimations I did not yet understand how difficult it could be to simply get setup where you can run tests and compile clojurescript to javascript. The process was a bit challenging and very new so I will briefly go over how I got my code to run.I followed a git repository by Michael Whatcott and he set up a project structure with necessary dependencies and files to help the ease of setting up a clojurescript project. This contained a detailed project.clj file or dips.edn  like this. 
```clojure
{cljsjs/react {:mvn/version "17.0.2-0"}
cljsjs/react-dom {:mvn/version "17.0.2-0"}
reagent/reagent {:mvn/version "1.1.0"}
com.cleancoders.c3kit/apron {:mvn/version "1.0.2"}
speclj/speclj {:mvn/version "3.4.3"}
}
```
Another important piece, is a runner folder that contains a cljs.clj file that interacts with a run command file to help compile the cljs files to javascript. The runner file is always called when building the project and this will generate all necessary files like the main javascript file that contains your code.Outside of additional files it is important to have the correct extension on your clojure files. If it is purely clojurescript it can be named with a .cljs extension but if it needs to be required in a clojurescript file but also a Clojure file then it should be named with a cljc. This means it can be compiled as clojure or clojurescript.  This is just the absolutel barebones of setting up a clojurescript project and I will go into more details and more aspects of it in another post. 
