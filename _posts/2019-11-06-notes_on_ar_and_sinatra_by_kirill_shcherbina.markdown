---
layout: post
title:      "NOTES ON AR AND SINATRA by Kirill Shcherbina"
date:       2019-11-06 19:12:33 +0000
permalink:  notes_on_ar_and_sinatra_by_kirill_shcherbina
---


**What is Rack?**

Rack is the underlying technology behind nearly all of the web frameworks in the Ruby world. "Rack" is actually a few different things:

*An architecture* - Rack defines a very simple interface, and any code that conforms to this interface can be used in a Rack application. This makes it very easy to build small, focused, and reusable bits of code and then use Rack to compose these bits into a larger application.

*A Ruby gem* - Rack is is distributed as a Ruby gem that provides the glue code needed to compose our code.

**What is ActiveRecord?**

Active Record is a gem which acts as the M of MVC. Model. When applied to a class it maps the objects of the class to a database. The objects get stored on a table. Therefore over there is the right place where to establish the association between objects. Has many, belongs to, etc.

**Sinatra**

Sinatra is a gem. It’s framework for Ruby. Frameworks are meant to make it easier to create big things. LIke websites, etc. There’s a lot of common code, and frameworks do that for you. So in essence Sinatra is the C of MVC. It’s the controller. 

Sinatra is a DSL -  Domain Specific Language implemented in Ruby that's used for writing web applications. Created by Blake Mizerany, Sinatra is Rack-based, which means it can fit into any Rack-based application stack, including Rails. It's used by companies such as Apple, BBC, GitHub, LinkedIn, and more.

Essentially, Sinatra is nothing more than some pre-written methods that we can include in our applications to turn them into Ruby web applications.

**How is it different than Rails?**

Rails is big. Its so powerful that it makes creating apps look like magic. Sinatra is much lighter. Meant for small simple apps. 


**What are Controllers?**

Controllers define an HTTP method using the sinatra routing DSL provided by methods like get and post. When you enclose these methods within a ruby class that is a Sinatra Controller, these HTTP routes are scoped and attached to the controller.

Controllers must be mounted in config.ru. [The purpose of config.ru is to detail to Rack the environment requirements of the application and start the application]. Mounting a controller means telling Rack that part of your web application is defined within the following class. We do this in config.ru by using run Application where run is the mounting method and Application is the controller class that inherits from Sinatra::Base and is defined in a previously required file.


**What are Routes?**

Whenever someone types in a URL, submits a form, etc, they are actually sending a HTTP request to a specific URL in your app. Routes connect the request to the specific part of the program that is being requested. They do this by matching the web request sent by a client to some code in our application that tells the app what data and templates to send back to the client. The get , or the post, or delete methods for that matter, will be invoked if Sinatra matches the HTTP method (GET, POST, etc) and the URL to a route defined in the controller.


**MVC - MODELS, VIEWS, CONTROLLERS**

The Model-View-Controller paradigm is a popular way of building frameworks for web applications - it provides a separation of concerns where groups of files have specific jobs and interact with each other in very defined ways. In a nutshell:

Models: The 'logic' of a web application. This is where data is manipulated and/or saved. 

-In Sinatra, models are generally written as Ruby classes. Models can also connect to databases to persist data.

Views: The 'front-end', user-facing part of a web application - this is the only part of the app that the user interacts with directly. Views generally consist of HTML, CSS, and Javascript.

-In Sinatra, views are written as .erb files, consisting of HTML and embedded Ruby (Ruby code written within HTML). They are what the user actually sees when they use your web application.

Controllers: The go-between for models and views. The controller relays data from the browser to the application, and from the application to the browser.

-In Sinatra, controllers are written in Ruby and consist of 'routes' that take requests sent from the browser ("GET this data", "POST that data"), run code based on those requests by using models, and then render the .erb (view) files for the user to see.


**BCRYPT AND SECURING PASSWORDS**

Bcrypt is a gem which helps encode passwords. Is ‘salts’ them. Salting means to manipulate them in such a way in which they cant be reverted to the original password. 

**Using Bcrypt**

In your table do the following:

```
create_table :users do |t|
     t.string :username
     t.string :password_digest
   end

```


 update our user model so that it includes has_secure_password

```
class User < ActiveRecord::Base
 has_secure_password
end
```


Note that even though our database has a column called password_digest, we still access the attribute of password. This is given to us by has_secure_password. 

```
post "/signup" do
 user = User.new(:username => params[:username], :password => params[:password])
end
```

Because our user has has_secure_password, we won't be able to save this to the database unless our user filled out the password field. Calling user.save will return false if the user can't be persisted.

```
post "/signup" do
 user = User.new(:username => params[:username], :password => params[:password])
 
 if user.save
   redirect "/login"
 else
   redirect "/failure"
 end
end
```


This would redirect the user to /failure if password field was left blank.


When we used has_secure_password we also invisibly used authenticate. So now we can run authenticate to check if our password matches to password_digest. Like in the code below:

```

post "/login" do
 user = User.find_by(:username => params[:username])
 
 if user && user.authenticate(params[:password]) 
   session[:user_id] = user.id
   redirect "/success"
 else
   redirect "/failure"
 end
end
```


