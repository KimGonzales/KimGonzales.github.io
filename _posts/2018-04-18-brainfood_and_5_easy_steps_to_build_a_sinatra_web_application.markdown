---
layout: post
title:      "Brainfood and 5 Easy Steps To Build a Sinatra Web Application. "
date:       2018-04-18 21:19:50 +0000
permalink:  brainfood_and_5_easy_steps_to_build_a_sinatra_web_application
---


Four months ago I had no idea how the internet worked. This week, I’ve built my first ever Sinatra web application from scratch.

### The App: BrainFood
[Source Code](http://https://github.com/KimGonzales/brainfood)

The benefits of reading include memory improvement, vocabulary expansion, stress reduction, and the reduction of the chances of developing Alzheimers. 

As student eager to connect with others through knowledge, I decided to dedicate my first web application to the advantageous activity of reading. 

Brainfood is a web app that utilizes the Model-View-Controller software architecture. It’s domain models are comprised of users, books and bookshelves.

Once a user logs in or signs up to the app, they are greeted with inspirational quotes from the most recent books posted. 

Users are able to catalog their most recent or favorite reads by creating new bookshelves and then adding books to them. They are also able to edit and update this information. As an added bonus, each user can browse other user Libraries for recommendations or inspiration. 

![Imgur](https://i.imgur.com/B8lXbCY.png)

###  5 Easy Steps to Get Started with an MVC Sinatra Web App Using an Active Record Database
Luckily, it's very easy to [Use Bundler with Sinatra](http://bundler.io/v1.16/guides/sinatra.html). 

**1.) Create a gemfile and add the required gems:**
 
```
source 'htttp://rubygems.org'

gem 'sinatra'
gem 'activerecord', :require => 'active_record'
gem 'sinatra-activerecord', :require => 'sinatra/activerecord'
gem 'rake'
gem 'require_all'
gem 'sqlite3'
gem 'thin'
gem 'shotgun'
gem 'pry'
gem 'bcrypt'
gem "tux"
gem 'rack-flash3'
gem 'sinatra-redirect-with-flash'
...
```

**2.) Set up the *config.ru* file to load your MVC environment, bundler and database connection before it runs the application. **

file: config.ru 
```
require './config/environment'

use Rack::MethodOverride
use [yourcontrollerA]
use [yourcontrollerB]

run ApplicationController
```

file: config/environment.rb
```
ENV['SINATRA_ENV'] ||= "development"
require 'bundler/setup'
Bundler.require(:default, ENV['SINATRA_ENV'])

ActiveRecord::Base.establish_connection(
   :adapter => 'sqlite3'
	 :database => 'db/#{ENV['SINATRA_ENV']}.sqlite'
	 
require_all 'app'

```


**3.) Create your MVC App with the following file structure:**

![Imgur](https://i.imgur.com/NGVl5AW.png)


**4.) Configure your Application Controller to inherit from Sinatra::Base, load your views/public styles sheets, enable sessions and session secret for user login and password functionality and rack flash for messages. **

```
require 'rack-flash'
class ApplicationController < Sinatra::Base

  configure do 
    set :public_folder, 'public'
    set :views , 'app/views'
    enable :sessions
    use Rack::Flash
    set :session_secret, "password_security"
   end
	end
```



**5.)Run 'bundle exec rackup' in terminal to start your server!**
You should see the following output in terminal:

![Imgur](https://i.imgur.com/slTExgS.png)

and this view when you open that port in your browser.

![Imgur](https://i.imgur.com/LOrSUMX.png)

That's It!

You've successfully set up your Sinatra Web App by connecting it to a server and now the fun begins.

Start building your models and migrations and don't forget to visit Brainfood for a little inspiration. 








