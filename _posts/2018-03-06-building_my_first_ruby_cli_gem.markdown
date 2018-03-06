---
layout: post
title:      "Building My First Ruby CLI Gem"
date:       2018-03-06 22:48:52 +0000
permalink:  building_my_first_ruby_cli_gem
---

### What I Thought, What I’ve Learned and What I Wanted to Give up On.

#### “Where to begin?!”

That was my first thought after reading the requirements of my first portfolio project with The Flatiron School. 

This assignment required us to build a CLI application that accesses data from any website of our choice, and then allows users to dig into another layer of the initial information that’s provided. 

It is meant to test our knowledge of Object Oriented Ruby essentials including topics like the object self, object relationships, collection iteration, variable scope and good old web scraping.

The lectures on how to begin building our CLI Ruby Gem suggested we start with the conception of an idea. 

As programmers at Flatiron we are taught to ‘build the code we wish we had.’

I decided I was going to build an application that brought the most up-to-date job postings to the user. But not just any job postings.. 

Two months ago, I started studying web development because I wanted to spend my life building cool applications while traveling the world. What better way to do that then to nab a remote job coding?!

#### Enter: Digital Nomad Jobs!

My application would scrape [RemoteOk.io](http://‘remoteok.io') and bring the newest web developer and design job postings to the gem user.

#### How would It work?
Once I knew what the gem’s purpose was going to be, I started brainstorming on the gem’s control flow. 

![Imgur](https://i.imgur.com/65uWVPU.png)

From there, I worked out a detailed outline of each class. I would create a CLI, a Job, a Company and a Scraper Class. I then outlined what attributes each class would have and what methods and responsibilities each would maintain. 

#### Class Architecture

![Imgur](https://i.imgur.com/6nDdM0q.png)
![Imgur](https://i.imgur.com/6RaGmND.png)
![Imgur](https://i.imgur.com/CfG0LLI.png)
 

#### Putting in The Work
Rather than starting from complete scratch - I used [Bundler](http://http://bundler.io/) (what a gem!)  like Avi demonstarted in the lecture and the project file structure, and git init was automated for me. 

Once I set up the right enviornment and confirmed that my files were being required properly I began hacking away with the CLI, Scraper and Job class. 

After writing the class outlines to reference from, the code poured out of me. I was impressed! 

During the last few weeks before coming up to the 'final projects' section,  I had struggled to understand certain concepts (namely object relationships) so I found myself going back to review lessons and read extra resources frequently.

**Last Friday night I stayed up until 6am having THE BEST TIME coding the CLI and Job class of this Gem. That was the moment I knew that putting in that extra time paid off.** 


#### The Challenges

For me, the main hardship of writing this gem was the scraping. There were definitely times where I just wanted to ask someone 'WHAT IS THE CODE??' 

Now, I am SO happy I didn't. If I did - if i just got that answer frrom someone else, it wouldn't have been such a great learning experience. Plus the feeling once I DID do it successfully was 100% worth it. 

It took me close to 8 hours just to scrape the webpage correctly, but I completed Digital Remote Jobs over the weekend.


#### Wrapping Up

Now I am just putting the final touches before publishing my first Ruby Gem to [Rubygems.org](http://rubygems.org). 

You can find the source code for Digital Nomad Jobs here [on github.](http://https://github.com/KimGonzales/digital_nomad_jobs) Check it out!

Enjoy it as much as I did making it. 

If you are reading this as another student who is just starting out on the CLI Gem Project - BEST OF LUCK! I hope you have a blast building it. For me, it's been one of the best learning experiences so far. 







