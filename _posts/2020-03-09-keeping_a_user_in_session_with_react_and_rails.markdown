---
layout: post
title:      "Keeping A User in Session with React and Rails"
date:       2020-03-09 14:27:11 +0000
permalink:  keeping_a_user_in_session_with_react_and_rails
---


I want to share my solution for keeping a user in session, even on page refresh, specifically for a React / Rails application.

My most recent project called “Memes vs Gifs” features a React.js front end and a Rails API back end. When I wired up my user sign up and login functionality, I realized that the session ID I was recieving from Rails wasn’t persisting when the page reloaded. An awesome feature of React is that every time you save a change in the editor, it automatically updates the virtual DOM, which refreshes the browser’s DOM. Unfortunately, this React feature isn’t helpful when you need a user to stay logged-in so you can keep testing its functionality and behavior!

First I created a custom action in my Rails API user controller.

app/controllers/api/v1/users_controller.rb
![](https://miro.medium.com/max/990/1*yV8e4t4NllWHVXtJyCOXdw.jpeg)

The action, current_user, will simply look for a user’s matching session ID and render the user object back as json.
Next, create a custom route that points to the current_user action, in Routes.rb. (Be mindful to place this route in the correct namespace.)

config/routes.rb
![](https://miro.medium.com/max/888/1*KHY9SuY158xUkKvx2sbrTg.jpeg)

Now I have an endpoint, /current_user, to fetch to from the React front end.
In React I create a new action that simply fetches to our new route and grabs the user object.

src/actions/users.js
![](https://miro.medium.com/max/895/1*9qvd_MJQuoMAJ29uboB4ow.jpeg)

The line: dispatch({ type: SET_USER, payload: userObj }) is the same action type that my fetch to my login route utilizes. In other words, I’m setting my current_user in state as the same user object that was set in state when that user logged in.

(Just in case, let’s see that reducer action type)

src/reducers/users.js
![](https://miro.medium.com/max/853/1*O40-Xkz7Q1cJIKZu03WNgw.jpeg)

And finally, we need to call our function, setCurrentUser(), that we exported from our user actions file. I call mine in App.js, the top-most level of my React components, which instantiates the rest of my app and components.

src/App.js
![](https://miro.medium.com/max/381/1*i6Hi-XpR1h3SR3L4xew1wg.jpeg)

The function gets called inside componentDidMount(). Therefore, whenever the page refreshes (the App.js component mounts to the DOM), setCurrentUser() will be called and our user object that carries the session ID will populate state and remain logged in.

Simple but effective!

Some tips and tricks: it’s a good idea to have a “loggedIn: false” in the user reducer, as initial state. When a user signs up, logs in, refreshes the page, or logs out, the state of loggedIn changes with each behavior. Keep an eye on your Redux dev tools during this process to make sure each action of user logging in, out, signing up, and refreshing the page sets the loggedIn boolean to the correct one.
