---
layout: post
title:      "Rails Project: Mealzys (a meal prep manager)"
date:       2019-09-23 09:04:58 -0400
permalink:  enter_your_title_here
---


I learned a lot on this project. I learned "what not to do" just as much as integrating the necessary components to build a basic rails website. 

First and foremost, I wish I had started with OmniAuth, building out my models to include the appropriate User attributes, and created my models and controllers around whichever Social Login I was using, which happened to be Google. In fact, it was one of the last things I integrated into my project, and I spent way too long changing my schema, migrations, models, routes and controllers in order to let users sign in with their Google accounts. 

So word to the wise: decide which social login service you want to use, and start with that! It will save you a ton of time. 

One thing I really enjoyed was integrating a scope method to help sort my user's recipes by meal type: breakfast lunch and dinner. This was my first time using a scope method and while it took me some hard googling to make it work, I love their versatility. I wrote a dynamic method... scope: food_by_meal, -> (meal) {where(meal: meal)} ...based on my recipe's meal attribute (here it is in my controller).

![](C:\Users\james\OneDrive\Pictures\Screenshots\Recipe Model Scope.png)

```
class Recipe < ApplicationRecord
    belongs_to :user
    has_many :recipe_ingredients
    has_many :ingredients, through: :recipe_ingredients

    validates :name, uniqueness: true
    validates :name, presence: true

    scope :food_by_meal, -> (meal) {where(meal: meal)}

end

```

And then in my views, I tell it took look for a recipe by it's meal type attribute, and with some helper methods to downcase and then humanize (make the beginning of a word capital), I can sort each meal into the appropriate part of my index view page.

```
<h1>Your Recipes</h1>

<section class="todoapp">
	<section class="main" style="display: block;">
		<ul class="todo-list">

            <h3><font color="CornFlowerBlue">Breakfasts:</font></h3>

            <%= render partial: "recipe_meal", locals: {meals: @recipes.food_by_meal("breakfast") } %>

            <h3><font color="CornFlowerBlue">Lunches:</font></h3>

            <%= render partial: "recipe_meal", locals: {meals: @recipes.food_by_meal("lunch") } %>

            <h3><font color="CornFlowerBlue">Dinners:</font></h3>

            <%= render partial: "recipe_meal", locals: {meals: @recipes.food_by_meal("dinner") } %>

        </ul>
	</section>
</section>

<p><%= button_to "Create a Recipe", new_recipe_path, :method => "get" %></p>

<p><%= button_to "Homepage", root_path, :method => "get" %></p>

```

![](C:\Users\james\OneDrive\Pictures\Screenshots\Recipe Views Index.png)

Overall, this project gave me a good deal of headache, but I also learned a lot about setting up the environment, debugging in the terminal, playing with objects in the console, reading errror messages from the server/browser, and good old fashioned Googling. 

I had to jerry-rig some functionality into my app that Rails alone can't provide, and that JavaScript will dramatically improve the user experience. But for now, I am proud of what I made, and I am looking forward to the next section and incorporating more front-end elements into my Mealzy's food prep managing website.
