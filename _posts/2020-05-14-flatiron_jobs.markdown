---
layout: post
title:      "Flatiron Jobs"
date:       2020-05-14 13:47:12 +0000
permalink:  flatiron_jobs
---


Phew. That was a ride.

Typing in “git push” to my terminal for the last integral feature to the project, a feeling of relief washed over me. I was (for now) done with my first project at Flatiron. All of my fears, my concerns, my stress, all of it fell to the wayside. I had done it. I had made my first original Command Line Application (CLI).

At the very beginning of the project, my visionary nature got the best of me. What had originally intended to be a simple job finding application (titled “Flatiron Jobs”) had turned into a behemoth of overengineering and design, complete with ambitions of saved job persistence, multiple user profiles, incredibly detailed information views, and more. This was my debut, the very first project I had made and expected to be under the scrutiny of other people. In other words, this was the first impression I’d give, and I wanted to knock it out of the park with all the possible bells and whistles I could add.

Safe to say, I didn’t knock it out of the park. Not with those all-important bells and whistles, at least. 

As I thought about my approach going into the project, the core of the project’s functionality, the necessary features needed to at the very least make a MVP (minimum viable product), slowly started to come into focus. It didn’t present itself to me in an immediate moment of clarity, but the general outline was there. It was a matter of coaxing the details out of the obscurity of the vision I had, rather than just going in with a well defined plan and sticking to it. 

My first goal when it finally came time to start implementing the code for the program was to get the Parser class working in a solid, functional state; without it, I wouldn’t have a good foundation to build the CLI around. Upon meeting with my cohort lead, we were able to work through and design the first class method: the get_results method. This method was to act as the initial fetch from the Github Jobs API, returning an array of hashes which each acted as containers for four critical components the user absolutely needed before a more detailed fetch could be performed. These components would allow the user to preview each job posting that matched the user’s search criteria by getting details such as the job title, the company name, and the job description, as well as the specific Github Jobs URL (which we’ll fetch more information from later). After that method was implemented, I returned to the interface of the application. 

Despite its name, the cli.rb file does not contain the actual core logic of the interface. Instead, the CLI’s logic is contained within the JobFinderController class, which cli.rb calls upon in order to get things kicked off. In the submitted version of the project, the Job Finder Controller starts with presenting a main menu to the user, but at this early stage it just went straight to the job search method. The first thing this method does is prompt the user for three important bits of information: the user’s preferred job title or expertise, the user’s preferred job search location, and whether or not the user wants to restrict their search to full time jobs. After all of those are obtained and are checked to be valid inputs, the method passes those values to the Parser method we defined earlier, getting back a list of highly personalized results. 

It was from here that the application finally started to really take shape. Creating the foundation first in the form of the Parser and JobFinderController classes instead of defining other classes, such as the Job and User class, allowed me to return to those other classes later and know exactly how each and every one should interact with each other. In other words, treating them like black boxes and putting the core design of the application first ended up saving me tons of valuable time, and may be an approach I’ll return to in the next project. All in all, doing this project was extraordinarily fun and fulfilling, and I can’t wait to apply what I’ve learned from this one to the next!

