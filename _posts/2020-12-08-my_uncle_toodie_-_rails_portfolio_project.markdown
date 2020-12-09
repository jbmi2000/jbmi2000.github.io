---
layout: post
title:      "My Uncle Toodie - Rails Portfolio Project"
date:       2020-12-08 23:06:21 -0500
permalink:  my_uncle_toodie_-_rails_portfolio_project
---


#### Everybody has one I suppose  

They are common fixtures in most families.  You know who I mean...that aunt/uncle that comes around during the holidays, who seems to know everything about everything.  As much as you would love to refute it, these people have the answer for every question; sometimes before you even get  a chance to ask it.  They have had life experiences, so they know how to keep you from making mistakes.  If you're involved in something, no matter what it is, that aunt/uncle will have the cure for what ails.  They are the self-proclaimed subject matter expert for all.  You love them, and even though you're tempted to roll your eyes when they start talking, something tells you to keep listening because, most of the time, their advice is very much needed.

#### Let's call him Toodie

For me, it's my uncle "Toodie" who knows all and tells all, even if you don't ask.  I don't actually have an uncle Toodie.  I've just renamed him for protection and to avoid compensating him for using his name.  Uncle Toodie has life lessons about education, careers, plumbing...you name it!  I would give you an example, but that's not quite the intention of this blogpost, now is it?

#### Rails Knows

During this project, the one aspect of Rails that stands out to me is the 'done-for-you' theme that keeps recurring, like the form builder that is generated with the `form_for`, or how the command-line code `rails g model ` which is automatically interpreted as `rails generate model`, creates a new class is automatically, that inherits from ApplicationRecord.  My favorite done-for-you is resources.  

Just like my Uncle Toodie, Rails knows that, when you're building a project particularly with the MVC framework, you're going to need to build restful routes that will be used to communicate with the controller actions to handle passing information back and forth between the models and views.  Instead of making us write out each restful route manually, Rails has the `resources` code.  When executed, Rails will automatically create the restful routes, INDEX, NEW, CREATE, SHOW, EDIT, UPDATE, & DELETE for the specified model, using the appropriate HTTP verbs.  

```
Example:

resources :client
```
generates the following restful routes for the Client class along with associated paths:

```
GET	/client	client#index
GET	/client/:id client#show
GET	/client/new	client#new
POST	/client client#create
GET	/client/:id/edit client#edit
PUT/PATCH	/client/:id	client#update
DELETE	/client/:id client#destroy
```

All we have to do is add the corresponding controller actions and we're ready to build out the views with forms and whatever else is needed:

```
def index
end

def new
end

def create
end
....etc
```
And for those special times when you only needs a few routes, you can specify which ones you need:

`resources only: [:new, :create, :show, :destroy]`

This will only generate the routes for the actions specified.  So the code above will not generate routes for EDIT UPDATE or INDEX.

For this project, I utilized the resources code in the following way:

```
resources :client
resources :stylist, only: [:new, :create, :edit, :update, :show]
resources :appointment, only: [:new, :create, :edit, :update, :destroy]
```

#### Lastly

Just in case you need to recall the generated routes, you can browse to localhost:3000/rails/info/routes.  This will give you a list of all generated routes and their associated paths.

```
stylist_index_path	POST	/stylist(.:format)	stylist#create

new_stylist_path	GET	/stylist/new(.:format)	stylist#new

edit_stylist_path	GET	/stylist/:id/edit(.:format)	stylist#edit

stylist_path	GET	/stylist/:id(.:format)	stylist#show
```

So I know what you're thinking..."This guy thinks Rails has a life of it's own".  Not really.  I know it's a coding language that was created by humans, ha!  It's just nice to know that the needs of software engineers were anticipated during creation.  I think uncle Toodie would approve!  :) 
