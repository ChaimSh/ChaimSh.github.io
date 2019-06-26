---
layout: post
title:      "MY CLI PROJECT"
date:       2019-06-26 01:50:35 +0000
permalink:  my_cli_project
---

*BY KIRILL SHCHERBINA*

The project scope comprised of using Object Oriented Ruby to create a command line interface (CLI) to access data that is scraped from a website. The data that is being accessed is two levels deep; a level refers to where a user can choose an option and then receive more information about their choice.

# The Idea
I decided to choose a topic of my interest, Daily Study of Torah ideas and laws. My thought was to create an application that givees oyu the ability to just pop onto your screen the content of today's daily lesson. I used Chabad.org to scrape. I looked to make sure this site's content was totally scrapable. Which it was. So I scraped off two daily study lessons. Then created a secind level by offering to recieve extra content.


# The Project layout
To provide separation of concerns, I created separate classes for CLI, DailyStudies and DailyStudiesScraper. I first made a rough outline of the DailyStudies class so I would  have a better idea of what information I wanted it to contain. The DailyStudies class is responsible for initializing each class object with a name, credits, text and full_text which are then saved to the @@all class variable.

```
  
 attr_accessor :name, :credits, :text, :full_text
  
  @@all = []
  
 def initialize(name, credits, text, full_text)
  @name = name
  @credits = credits
  @text = text
  @full_text = text
  @@all << self
  end
  
  def self.all
    @@all
  end
```

My Scraper class is responsible for scraping all of the data from the website to get the write daily lesson. By parsing I was able to get the attributes specified in the DailyStudy class. I then created a second level by asking the user if they would like to see more content. Upon pressing y they would get to view more content. 


```

  def self.rambam_scrape
    doc = Nokogiri::HTML(open("https://www.chabad.org/dailystudy/seferHamitzvos.asp?"))
    
    rambam = self.new
    rambam.name = doc.search("h3.article-header__subtitle").text
    rambam.text = doc.css("div.co_body p").text
    rambam.credits = doc.search("div.credits").text
    rambam.full_text = doc.search("div.co_body.article-body").text.strip
    rambam
  end
  
```


Then i passed the content of the scrapers into a an array. Calling .each on them to print the proper content at the proper time and place and finally this was set in a proper loop so the user always has an option to either continue or exit and if entering a non-option would be notified. 

Thank you for reading. Hope you enjoyed!

*-Kirill Shcherbina*
