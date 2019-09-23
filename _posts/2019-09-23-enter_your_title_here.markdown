---
layout: post
title:      "Enter your title here"
date:       2019-09-23 13:04:57 +0000
permalink:  enter_your_title_here
---


I learned a lot on this project. I learned "what not to do" just as much as integrating the necessary components to build a basic rails website. 

First and foremost, I wish I had started with OmniAuth, building out my models to include the appropriate User attributes, and created my models and controllers around whichever Social Login I was using, which happened to be Google. In fact, it was one of the last things I integrated into my project, and I spent way too long changing my schema, migrations, models, routes and controllers in order to let users sign in with their Google accounts. 

So word to the wise: decide which social login service you want to use, and start with that! It will save you a ton of time. 

One thing I 

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
