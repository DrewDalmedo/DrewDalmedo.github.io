---
layout: post
title:      "The VGC Project"
date:       2020-06-08 20:01:46 +0000
permalink:  the_vgc_project
---


If Flatiron Jobs was a ride, VGC was an absolute rollercoaster.

VGC, otherwise known as "Video Game Collector" is a web app that I built with Sinatra that is designed to help users manage their collection of video games and video game consoles. In more technical terms, it's a CMS (content management system), pure and simple. 

There was a whole lot of new information to keep track of when I was going into this project. For instance, what's the MVC paradigm? How do you use ActiveRecord to manage a database? RESTful routing? Database migrations and seeding?? HTML?!

...yeah, there was a lot to know.

However, with one project already under my belt, I knew what my limitations were. I improved upon my previous mistakes and designed an app that was *actually doable* with the given timeframe, which was a week. I kept it simple, electing to create a MVP (minimum viable product) rather than adding all the bells and whistles I initially came up with while designing it.

The first and foremost thing I did when I started working on the project was create a database to hold user data. This included their usernames, their emails, and their salted passwords. Note that I said salted. **NEVER** STORE PASSWORDS AS RAW TEXT! I'll talk more about securing passwords later on.

After creating the user database, I got to work on creating the main application controller and the users controller. The main purpose of *any* controller is to contain the logic which your web app needs to function. This includes how to react to the user going to a specific url, what to do when a user submits information, and so on. The function of the main application controller is to configure all the miscellaneous settings of the web app, from setting the views folder directory to enabling sessions. Enabling sessions allows the web app to use cookies, which in turn allows the user to leave the website and still be signed in when they return to it. These cookies are secured with a cryptographic key, often randomly generated and kept out of the code which is available publicly. In the case of my project, I decided to keep the key in the publicly available code, as this project isn't meant for production / public use. If the web app were to be used publicly, the key would have to be kept on the server running the web app only, and not in the public GitHub repo.

In addition to configuring those settings, the main application controller also contains the logic for when people first visit the site. It loads a view created with ERB, which stands for "Embedded Ruby". ERB allows for a mix of HTML and Ruby, which allows for websites to be dynamic and interpret ruby code as the site loads.

Next there's the users controller, which holds all the logic of how to sign in, register, and view account pages, in addition to processing all the information submitted by the browser. This class was particularly light, as user to user interactions aren't a focus of this app. 

Finally, there are the two different controllers which contain the core logic to the central parts of the web app: the games controller and the console controller. These two controllers handle the creation, viewing, editing, and deletion of a user's games and consoles. 

None of this would be possible, however, without the three models I used. These all corresponded to the different controllers that I listed above, so there's a user model, a game model, and a console model. Remember when I said that I'll talk about securing passwords later on? This is where that comes into play.

In the user model, there's one important line that makes the passwords users provide secure: `has_secure_password`

Yes, it's that simple.

The mechanics of how the password is secured is handled by ActiveRecord (see [the docs](https://api.rubyonrails.org/classes/ActiveModel/SecurePassword/ClassMethods.html) for more info). The short version is that it uses a password hashing function called "bcrypt" to turn the password into a string of random bits, and after it transforms the password into that string of random bits, it stores it in the database as "password_digest". 

If you want to see more about my project and how I implemented it, please check out it's GitHub repo here: https://github.com/DrewDalmedo/vgc
