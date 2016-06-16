---
layout: post
title:  "Building A Command Line Interface (CLI) Gem with Bundler"
date:   2016-06-16 18:09:22 +0000
---


**Ok!** So the first thing you want to do when building a gem, or anything code related, is to create a new git repository with your project name. This is crucial to keeping track of your program’s development and giving yourself credit for your work. The next thing you want to do is open up your repo in terminal so you can get to work on it. I cant really see a scenario where not having Bundler was a great idea for a rubyist, so I’m just going to assume every ruby programmer has it and move on. If you don’t have it installed you should because it makes life a bazillion times easier (http://bundler.io/). Once Bundler is installed, the only thing you have to do to create a gem is type “bundle gem” and then your gem name inside of your repo. Your gem name should generally be the name of your repo, and should not contain dashes or spaces, as that can mess with your folder structure…but underscores are ok.

The next thing you want to do to create your gem is to open up the repo with a code editing app. Any will do, but I use Sublime Text 2, and thus can type “subl .” to open the folder in Sublime. Looking through the folder structure you will notice 2 folders (bin and lib) and a bunch of other files. The bin folder is for executable files, and inside the lib folder is another folder (working folder) with your gem name where most of your code will go. Also inside the lib folder is a ruby file (.rb) with your gem name where you will begin coding. In this file you want to type the following:

require_relative '../config/environment'

That’s it! In fact if there is anything else there, you can delete it. The purpose of this line is to make it clear for developers where your gem’s dependencies are. You can now save this file and never come back to it…Yaaay! However (lol), you will be using another file in its place. The next step in building your gem is to go out to the main folder, and create a “config” folder next to bin and lib. Inside the “config” folder you’ll need to create an “environment.rb” file where you’ll put all your gem’s dependencies. Here you will use “require” to include other programs in your program and “require_relative” to include files within your program throughout your program. You will have to update this file every time you add a file to your working folder. (lib folder>Project folder>file).

The next step to completing your gem lies in the bin folder. You should have 2 files already in there (console and setup) that can be ignored. At this time you’ll need to add another file to the bin folder. You can name this file whatever you want, but remember to stay relevant to your gem (dashes are ok here). There is no suffix to this file, so don’t add (.rb). Your ruby program will understand what language it is written in when you add a “shebang” line to the top of your new file:

#!/usr/bin/env ruby

This line is only used in bin folder files and is only used so that bash may decipher your code. Next you’ll need to add a “require_relative” line that links to the file with your gem’s name on it inside your lib directory. This will link all the files in your program to the file in your bin folder, which is your executable file, and now you are all setup to build your wonderful program! For now though, I would suggest you simply print (or puts) a line of text (lorem even!), so that you know your program works when you try it. This will give you a chance to simplify the gem building process, and reduce the chance of you confusing yourself when something goes wrong…and it will! The last thing you’ll want to do to this file is change it’s permissions. Since you’ve just created the file it will probably have only read and write permissions, but this is an executable file so it needs executable permissions. To do that we need to go to the bin folder in our terminal and type:

Chmod +x your-file-name

This will add the exe permissions to your file. You can check it by typing:

Ls –lah

This will bring up all the files in the bin folder and tell you their permissions. As long as you see the letter x in your file’s permissions you should be good. Alright! So let’s assume your program is complete and error free and ready to gemify. The first thing you want to do is jump to your gemfile in your root folder. Here you’ll see the word “gemspec”. You’ll want to replace that with the following:

gem 'your_gem_name'

 I had an issue getting my gem to execute upon install, and this seemed to be the culprit. Next, looking in your gem’s root folder you should see a (.gemspec ) file with your gem name. Here you’ll find a lot of sections you’ll need to edit just to properly label the gem as yours, all of which are labeled with the term “TO DO”. There are however, 3 of these of particular importance. The first is labeled as follows:

spec.metadata['allowed_push_host'] = "TODO: Set to 'http://mygemserver.com'"

That needs to be changed to:

spec.metadata['allowed_push_host'] = 'https://rubygems.org'

This will allow your gem to be published, should you choose, to “[RubyGems.org](http://rubygems.org)”. The second and third are labeled:

spec.bindir       = "exe"
spec.executables   = spec.files.grep(%r{^exe/}) { |f| File.basename(f) }

That needs to be changed to:

spec.bindir       = "bin"
spec.executables   = ["your-exe-file-in-bin-folder"]

These changes will ensure a smooth execution when your file is installed and used. That’s all you need! Now to build your gem, go to your terminal, open up your gem folder then type:

gem build your-gem-name.gemspec

This will build a copy of your gem in you gem folder and package it for you. You’re technically done at this point, but it would be awesome if you published your gem online at “RubyGems.org”. If you setup your gemspec right earlier, all you need to do it type:

gem push your_gem_name-0.1.0.gem

The numbers are the version number of your gem, which can and need to be changed in the version.rb file every time you push a new version of your gem. This will prompt you for a password and username, which you get by signing up at “RubyGems.org”. If all goes well you’ve done it! You have now built and published a CLI gem with bundler.

Sign up here and get a $250 discount on Learn.co with the Flatiron School: learn.co/with/IshmaelKhalid

Other Helpful Tutorials:
1. http://railscasts.com/episodes/245-new-gem-with-bundler
2. http://guides.rubygems.org/
3. http://code.tutsplus.com/tutorials/gem-creation-with-bundler--net-25281

