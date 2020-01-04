---
layout: post
title:      "Buy / Where JavaScript Project"
date:       2020-01-04 23:57:35 +0000
permalink:  buy_where_javascript_project
---

https://github.com/jamesncox/buy-where

This is my second attempt at the JavaScipt project, having dropped back a cohort, because I really wasn't prepared the first time, and didn't understand a lot of what I was supposed to implement. I've come out this project the second time a lot more confident and stronger in not only JavaScript, but everything we've learned up to now.

My JavaScript project is called "Buy Where", which is a simple app that tracks whatever you purchase and where it is purchased. Buy Where allows you to easily add stores and items, and easily edit them.

I created a Rails API backend using RESTful convention to structure my Stores and Items models. A store "has many" items, and an item "belongs to" a store. 

In my Store and Item controllers, I make sure to "render: json" for all my controller actions. 

There are a lot of things I wish I could have implemented, like error messaging, a user login from a third party, validations, among a few other things. I have done those things in past projects, and wasn't a requirement of this project. But I still feel good about the frontend and what I learned and accomplished.

My frontend is built with HTML, CSS and JavaScript. 

My index.html file contains all the scripts for my JavaScript files, and the form for creating a new store. I have a little static HTML defining containers for my store cards, and the items associated with those stores. Otherwise, most of my DOM elements are defined and created in my JavaScript classes.

Index.js kicks off the app, where I call on my App class and instantiate with: new App().

App.js is where I define my App class and instantiate with a constructor my Stores and Items classes (not to be confused with my Store and Item classes).

Both my Stores and Items classes instantiate my adapters, which is where my fetch requests are defined. The bulk of my logic for Buy Where is in stores.js, because an item belongs to a store, and most of the fetch for both items and stores go through my StoresAdapter.js. However, I do use an items adapter for my create ("post") and update ("patch") fetch requests.

I faced many challenges with this project, and having dropped back a cohort to fully comprehend the components of this project, I had the good fortune to face those challenges twice over! 

Specifc challenges I face were: knowing which DOM elements to target when adding event listeners, and which JavaScript selector works best in various scenarios; I really struggled with dynamically created DOM elements, and debugging "null" values; defining my "patch" fetch requests to update an Item and making sure to include both the item id and store id; in fact, keeping all of my objects organized by their id's took a lot of practice, making sure to define them correctly with both HTML and JavaScript.

All in all, I am definitely more comfortable with JavaScript and functions! And for me, that's a win!



