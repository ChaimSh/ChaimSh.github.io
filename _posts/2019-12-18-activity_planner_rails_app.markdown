---
layout: post
title:      "Activity Planner Rails App"
date:       2019-12-19 00:59:21 +0000
permalink:  activity_planner_rails_app
---


BY CHAIM KIRILL SHCHERBINA

The Activity Planner App was built using Ruby on Rails framework and no scaffolding was used to build this project. This app was created with an intention to help users plan their events and organize activities.

My app is pretty simple. I created my own authentication and authorization methods without using gems like Devise and Pundit. In order to make the registration process easier, I have included a third party log in with a single provider Google. After logged in, the user can add activities and locations then relate them to an event that they will also add.

After adding either locations, activities or events, the user is taken to the show page, which lets them update. Only current users can see the displayed pages.

Here are the steps I used to create my project application.

**1- Creating the Application**
To create files with Rails just type on the terminal:
$ rails new app_name

**2- Install the Required Gems**
By default Rails applications manage gem dependencies with Bundler. I added the gems below to my gemfile.
gem ‘omniauth’
gem ‘omniauth-github’
gem ‘dotenv-rails’
gem ‘pry’
gem ‘bycrypt’
Run bundle:
$ bundle_install

**3-Create the Database**
Example of a table to create user table.

```
class CreateUsers < ActiveRecord::Migration[6.0]
  def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.string :password_digest

      t.timestamps
    end
  end
end
```

Use a rake command to run the migration:
$ rake db:create

**4- Create Models**
Here is an example of my app/models/user.rb file. I have added validations and to secure password, I included the gem bcrypt in my gemfile .
The has_secure_password adds methods to authenticate against a BCrypt password. This mechanism requires you to have a password_digest attribute. This is create to secure your app if you are not using gems to secure your app.

```
class User < ApplicationRecord
    has_many :activities
    has_many :locations
    has_many :located_activities, through: :locations, source: :activities 
    has_many :events, through: :locations
    has_secure_password

    validates :username, :email, presence: true
    validates :username, :email, uniqueness: true
end

```

These validations will ensure that students have a name, email, and password and that the email is unique to the student.

**5- Create Views**
Remember that view directly interact with the user. This is where I put all the code that makes my app look nice, and how my user sees and interacts with it . I used partials to simplify my views and to keep it dry. Partials are great tool for cleaning up layouts.


**6- Create Controller**
It’s the brains of the application, and ties together the model and the view. Here is where all the actions code goes.

```
class UsersController < ApplicationController
    skip_before_action :redirect_if_not_logged_in, only: [:new, :create]
    before_action :redirect_bc_logged_in, only: [:new, :create]
  def new
    @user = User.new
  end

  def create
    @user = User.new(user_params)
    if @user.save
        session[:user_id] = @user.id
        redirect_to user_path(@user)
    else
        render :new
    end
  end

  def show
    @user = User.find_by(id: params[:id])
  end

  private

  def user_params
    params.require(:user).permit(:username, :email, :password)
  end
end


```

 I learned a lot throughout the process! I hope this blog helps you with your project!
 
 Thank you!



