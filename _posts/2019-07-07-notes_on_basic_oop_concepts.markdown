---
layout: post
title:      "NOTES ON BASIC OOP CONCEPTS"
date:       2019-07-07 21:38:46 +0000
permalink:  notes_on_basic_oop_concepts
---


BY CHAIM KIRILL SHCHERBINA

**Class**
To illustrate with an example:
A Dog class produces individual dog objects, each of which contains all the information and behaviors of an individual dog.

Think of a class like a blueprint that defines how to build an object.

***Instance Methods***.
Instance methods are methods defined within the object’s class. We call them instance methods because they belong to any instance of the class. 

Example:  Defining #bark within the Dog class, bark becomes a method of all instances of Dogs. If we make more dogs, they can all bark.


Note: Instances of a class are not globally evocable like procedural methods. They cannot be called without an instance.

      .     
***** Initialize*****
The initialize method will require certain arguments to be passed when instantiating the class, to provide it with initial data. In other words, an #initialize method is a method that is called automatically whenever #new is used.

What we would have to do without initialize, after making a setter and getter for breed:
```
snoopy = Dog.new #=> #<Dog:0x007f970a2edfd0>
snoopy.breed #=> nil
snoopy.breed = "Beagle"
snoopy.breed #=> "Beagle"
```
And do this each time for each dog.

If we want each instance of our class to be created with certain attributes, we must define an #initialize method. 

You can also think of the initialize method as a constructor method. A constructor method is invoked upon the creation of an instance of a class and used to help define the instance of that class.





***Getter/Reader*** 

A Getter Method returns information stored in an instance variable. (Editor’s note: hence it can be read but not written, it only returns. So once set, can’t be changed).

***Setter/Writer***

A Setter Method allows the information in an instance variable to be ‘written’ ‘set’ ‘edited’.
- It is written with an ‘=’ after the name of the method. 
- Called using dot notation.
 

***Self***

Every object is aware of itself and we can define methods in which we tell objects to operate on themselves. We do so using the self keyword, inside the body of an instance method, to refer to the very same object the method is being called on.

Example: By a dog switching owners originally we had to write: 
```
def adopted(dog, owner_name)
 dog.owner = owner_name
end
```

But using #self we can refractor:
```
def get_adopted(owner_name)
   self.owner = owner_name
 end

```
            




***Instance Variables***
An instance variable is responsible for holding information regarding an instance of a class and is accessible only to that instance of the class.

***Class Variable***
Class Variables store information regarding the class as a whole. They are accessible to the entire class––they have a class scope.

A class variable looks like this: @@variable_name.

***Class Method***
A class method is a method that is called on the class itself, not on the instances of that class. They enact behaviors that belong to the whole class, not just to individual instances of that class. (note: this can be done because even classes are objects).

Example;
```
class Album
 @@album_count = 0
 
 def self.count
   @@album_count
 end
end
```
                 Now if we call:
Album.count
                 It will return 0.

Note: Part of knowing when to use a class method is looking who’s job is it to for example, keep track of those albums. Individual instances of albums or the whole album class? Obviously the latter.

