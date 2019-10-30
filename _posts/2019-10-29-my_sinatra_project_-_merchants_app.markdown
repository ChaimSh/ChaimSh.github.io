---
layout: post
title:      "MY SINATRA PROJECT - MERCHANT'S APP"
date:       2019-10-30 01:41:49 +0000
permalink:  my_sinatra_project_-_merchants_app
---


By Kirill Shcherbina

My game plan for the app is as follows: Once a user signs up (with a unique username and email) onto the website, the user is able to view other users’ product listings and has the ability to create a listing himself. Users must include the name of the product and price. Description, however, is totally optional. however suggested. Editing and deleting of other users' listings is prohibited. 

This app was built following the MVC (Models, Views, Controller) structure: 

**Controllers:** I have an application controller, customer controller and a product controller. 


**Models:** I decided to have a customer and product model, where the customer has many products and the products belongs to the customer.


**Views:** I knew that I would have an initial landing page, where a user would go when not logged in (welcome.rb). I also created layout.erb template, to avoid copying over basic HTML on every erb file. There would have to be views for the products- viewing, creating, and editing. And for users, a sign up page and a login page was crucial.

I tested out this application in the browser with the help of a gem called Shotgun, which allows you to refresh a page to see changes, no need to restart the local server.

Overall this project was a great learning experience for me. I have become more confident with creating a Sinatra App from the ground up and in my general coding skills. 
