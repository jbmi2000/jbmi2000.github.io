---
layout: post
title:      "The Art of Simplicity-Peace with Complexity:  CLI"
date:       2020-02-17 02:49:39 +0000
permalink:  the_art_of_simplicity-peace_with_complexity_cli
---


Kudos to India.Arie for providing the lyric that I stole for the title of this blog.  It's from her song titled "Wings of Forgiveness", and it talks about NOTHING technical, unless you're some sort of love scientist, so we'll move on.

**Simplicity - That Which is Simple**

In thinking about Object Orientation, the concept is relatively simple.  You create new instances of objects through a blueprint or factory object called a class.  Then you teach that object about itself, and about the "world" around it, by running mini programs called methods.  Each method plays a role in shaping the object's experience while in existence.   Simple, yes?  Well...

**Talk About Your Thick Plots**

If there was only one object in this Object Orientation "world" that gets created, well, that would make things pretty simple, if not painfully boring.  However, the magic behind OO is in the interaction between objects.  Things like the creation of methods that call other methods and store data for use at a later time, and the interdependencies of classes, gems, constants, variables, conditionals, booleans, parsing, iterating and testing and testing and...wait...Where was I?

Oh yes...the magic of Object Orientation...with all that is involved, it can be very exciting, and therein lies the complexity.  

This CLI Project is the perfect way to make use of all that is great about Ruby Object Orientation.  That does not mean it was easy, but certainly well worth the struggle, once the code is working.  My project is focused on providing a hair salon customer a way to see a list of available services and to book an appointment for those services.  This involved scraping data from an existing website.  I used the following code snippet:

```
 def self.scrape_services
        html = "http://cieloshairdesign.com/our_services"
        doc = Nokogiri::HTML(open(html))   
                
        doc.css("div.et_pb_text_inner h2").slice(0..3).each do |items| 
             name = items.text
             Hairsalon::Service.new(name)
        end
end

```

This is a method, #self.scrape_services, that exists in the Scraper class of the project.  It's purpose is to open the webpage saved inteh variable html, using the Nokogiri gem, and then saving the result in a variable called doc.  Once saved, the method will then iterate over the results and create new items to be stored in the @@all class variable in the Services class.  Those items are what comprise the list of services that are presented to the customer for selection.

**The Small Details**

One thing that I have learned from doing this project is that every character counts and 'pry' really is your best friend.  Pry is a wonderful little gem that allows you to interupt your code processing at a certain point, to test if that input will produce the desired result.  The trick is knowing where to place the "binding.pry" entry for the bset return.  Fortunately, you can move it around as needed.

Looking forward to the next round!
