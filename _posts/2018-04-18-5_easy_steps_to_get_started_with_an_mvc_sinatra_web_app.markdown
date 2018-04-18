---
layout: post
title:      " 5 Easy Steps to Get Started with an MVC Sinatra Web App"
date:       2018-04-18 21:23:01 +0000
permalink:  5_easy_steps_to_get_started_with_an_mvc_sinatra_web_app
---


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
