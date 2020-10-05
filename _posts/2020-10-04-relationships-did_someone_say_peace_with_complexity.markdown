---
layout: post
title:      "Relationships-Did someone say 'Peace with Complexity'?"
date:       2020-10-04 21:02:30 -0400
permalink:  relationships-did_someone_say_peace_with_complexity
---


Being a man of a certain age, I'd like to think of myself as fairly knowledgeable in the area of relationships.  After all, I've had several, the most recent of which is lasting over 23 years and counting.  With a stretch like that, some might even venture to say that I'm a bit of an expert in the subject.  I'm not ready to open up a counseling clinic, but I could probably hold my own in a discussion...maybe.

##### Along came Ruby

When I was first introduced to the concept of relationships between classes in Ruby, I thought "piece of cake! I got this!"  Ok, so I was wrong.  Although, I will say that understanding relationships is not as difficult as I once thought.  Knowing that there are many different types of class relationships is important, but moreover, how those different relationships effect the tools that your are given to allow your classes to interact.

There are several different types of relationships that can be used to allow class objects to take ownership and/or be acted upon by other class objects.  For the purpose of this blog, we will be briefly discussing the has_many/belongs_to pair. 

##### You Belong to Me

So I love that Carly Simon hit.  Though I'll admit to being  a bit more partial to the Michael McDonald and [Anita Baker](https://www.youtube.com/watch?v=DbKRrsDZ4MU) versions.  Granted, Ruby object relationships aren't quite as sensual, but hey, whatever helps the concept.  Ha!  

The *belongs_to* relationship is declared in a class that, by no surprise, will have objects that "belong to" objects of another class.  For my project, the Customer class has a belongs_to declaration as such:

```
class Customer < ActiveRecord::Base
      belongs_to :user
end
```

Making this declaration in the Customer class allows for the following methods to be called on an instance of the User class:

```
user.customers
user.customers=
user.build_customers
user.create_customers
```
These methods return arrays of information related to the many customers that belong to a single user.  Note that customers is plural here to fall inline with the typical companion declaration in the other related class, the *has_many*.  If a customer "belongs to" an instantiated user, then there must be some other relationship that connects the User class with the Customer class.  For the purpose of this project, that relationship declaration is the *has_many*.  

Just as it sounds, the has_many is saying that a single User object has many customers.  I should point out that, for this Sinatra project (Beauty Salon Customer Roster) the User class is creating user or Stylist objects.  So each Stylist will have many customers, based on the has_many declaration in the User class:

```
class User < ActiveRecord::Base
     has_many :customers
end
```

There are 13 methods that are gained with the has_many declaration, which I won't list fully here, but among them are the following:

```
customers.clear
customers.empty?
customers.size
customers.find(…)
customers.where(…)
customers.exists?(…)
```

One place where these declarations were helpful in the project was here, in the CustomersController:

```
get '/customers/index' do
        @user=Helpers.current_user(session)
        @customers = @user.customers
        erb :'/customers/index'
    end 
```

Here, in the route to display a user's customers, I was able to identify and store the current user through the Helpers.current_user method, into the @user instance variable, passing in the session infomation.  Then I called the .customers method on the current user (@user) and stored only their current customers in the @customers instance variable.  

What I learned here is that, there is always something to learn about relationships.  Admittedly, this is not quite as exciting as a first date, or being able to brag about a 23-year marriage, but when your code works, magic happens!  Am I right?
