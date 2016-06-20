---
layout: post
title:  "NewKS Project Class Walkthrough"
date:   2016-06-20 21:18:04 +0000
---


The (NewKS) gem is a revision of my (newest_kickstarter) gem, which is a simple command line interface (CLI) to access the top 20 newest projects on Kickstarter.com. This gem also allows you to receive basic information about those projects and a link to their project page. Its also pretty freaking cool that its sounds like “Nukes”…right?!

The project class is essential to my NewKS gem. It handles all of the scraping and defining of the projects in my list. At this point in the program, I have already referred to the project class several times in our CLI class. So far I have given it a (.all) method, which must be an array because I have also given it a (.each. and with_index) method, a (.find) method, and (attr_accessor) methods for name, summary, author, and URL. The first thing I have to do is to create my project class in its own ruby (.rb) file. Once my (NewKS::Project) class is setup I can go right ahead and add my (attr_accessor) methods for name, summary, author, and URL. Next I setup my (.all) method and (.find) method. The (.all) method is very easy. All I did was set the method name to (self.all), and inside that method I placed the (@@all) instance variable, that I set equal to our available projects, which must be scraped. For now I’ll just set it equal to the method name (scrape_newest_projects). The (.find) method is also very easy, because I can now use the (.all) method along with each projects index number to find that project. I set the parameter of the (.find) method to (id), and in the method typed (self.all[id-1]). This is essentially stating search all projects and find the project with this index number. The (-1) is crucial as indexes originally start at 0, but in the CLI class we started at 1.

The very last thing I did before I started scraping was to set my instantiation method. This is usually done first, but I wanted to hash out the items I knew before I tried anything else in this project. In this particular method my goal was to give every attribute of project a value, so I set them all to nil. This allows every project to have some values even if there are none for it on the scraped site. I also set each attribute equal to its instance variable, so that it may be stored in each instance of a project. 

The next step was to make my scrape method, which consisted of using Nokogiri on my chosen site, and setting the results to the variable (doc). Then I scraped my newly formed (doc) for a specific value (names) and set that to a variable. Lastly I used the (.collect) method to iterate through the names and collect the text and the URL into a new project instance. Each project instance instantiates with a name and URL, and this is how my projects are scraped.

At this point, I decided to go back and delete the summary and author values from the instantiation method, and to find those values in their own separate methods. I first set a (doc) method, with a (doc) instance variable set to each projects URL. Then I created summary and author methods with instance variables set to their location in their URL. And my Project Class was finished!

Sign up here and get a $250 discount on Learn.co with the Flatiron School: learn.co/with/IshmaelKhalid

