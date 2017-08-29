# Ankhbot Ruby Bot

## Note: While the chat functions of this bot are still functional, the DB connections are no longer possible due to encryption enacted in recent Ankhbot updates and, as such, the Rank Announcer functionality has been deprecated. The replacement for use in Ankhbot's new built in Scripting Module can be found here [Ankhbot Rank Change Announcer](https://github.com/HyperNeon/ankhbot-rank-change-announcer)

A quick command line Ruby bot I made to easily add some additional functionality to the awesome [Ankhbot Twitch Bot](http://www.ankhbot.com/)
You can check out the functionality on [Github](https://github.com/HyperNeon/Ankhbot-Ruby-Bot)
Here's a Demo: [Ankhbot Ruby Bot Demo](https://youtu.be/rP9o5Jm4lzI)

With this bot you can:
* Send and receive messages on the command line using your Ankhbot Bot Name
* Implement message listeners which respond in complex ways to user chat
* Monitor and send alerts/chat messages based on changes in Ankhbot data such as leveling up

Streamers using Ankhbot Ruby Bot:
* http://twitch.tv/gametangent

This is a work in progress, including the documentation. 

## Instructions

> This bot requires Ruby and was built with Ruby 2.4.0p0. Instructions for installing ruby are beyond this readme, but a good starting point is: https://www.ruby-lang.org I also recommend using [RVM](http://rvm.io) for Mac/Unix and, if you're on PC with Windows 10, running RVM inside the new [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about) because it's awesome! 

### Installation and Setup

First things first, and this should probably go without saying, but make sure you have already installed and configured [Ankhbot Twitch Bot](http://www.ankhbot.com/) Make sure you keep you copy down the twitch oauth key for your bot as you'll need that in setup later. Ankhbot doesn't actually need to be running for this to work, but the Ankhbot commands and it's data stores will not be updated if it's not, rendering much of the functionality here pointless. 

Clone the repository wherever you'd like to run your bot from:
```
git clone https://github.com/HyperNeon/Ankhbot-Ruby-Bot.git
```

Navigate into the new directory and then install the necessary gems:
```
bundle install
```
**Note:** If you don't yet have bundler installed then simply install it with `gem install bundler`

Copy the `settings-template.yml` file to a new file called `settings.yml` and update it with your configuration. This is where you will configure your twitch username/password, Ankhbot install folder, as well as string formatting for commands. Yaml files are simple text files so you can edit them with any text editor like notepad or via the command line below:
```
cp settings-template.yml settings.yml
nano settings.yml
```
Descriptions of the various config settings can be found in the settings file. 

### Running the bot
Once you've installed the required gems and updated the settings above, all that's left is to start up the bot. 
```
ruby ankhbot_ruby_bot.rb
```

It might take a few seconds, but you should see it start up and begin connecting to Twitch irc server. Once it's done writing the initial welcome message from Twitch you should be good to go. It will look like this:
```
hyperneon@HYPERNEONS-PC:~/Workspace/ankhbot-rank-announcer$ ruby ankhbot_ruby_bot.rb
:tmi.twitch.tv 001 robotangent :Welcome, GLHF!
:tmi.twitch.tv 002 robotangent :Your host is tmi.twitch.tv
:tmi.twitch.tv 003 robotangent :This server is rather new
:tmi.twitch.tv 004 robotangent :-
:tmi.twitch.tv 375 robotangent :-
:tmi.twitch.tv 372 robotangent :You are in a maze of twisty passages, all alike.
:tmi.twitch.tv 376 robotangent :>
:robotangent!robotangent@robotangent.tmi.twitch.tv JOIN #gametangent
:robotangent.tmi.twitch.tv 353 robotangent = #gametangent :robotangent
:robotangent.tmi.twitch.tv 366 robotangent #gametangent :End of /NAMES list
Connected... -->
```
**NOTE:** That you won't always see the last couple lines including the `Connected...-->` as Twitch doesn't always seem to send this but it should still be working. 

You can use this terminal as a normal IRC chat client if desired. Anything you type will be sent as a normal message from your bot when you hit enter. Any messages received from other users will be displayed as well. 

You can exit (stop) the bot by typing:
```
ctrl+c
```

### Rank Announcer and adding other commands

The Rank Announcer will monitor the Ankhbot database for any changes to the user ranks (found on the currency tab) and issue a message whenever a user levels up or levels down. It does this by keeping a copy of the users and ranks as of the last time it ran and then checking the current state against this. You can configure how often this runs as well as the text displayed and other configs in the `settings.yml` file. 

**NOTE:** The first time it runs it'll pretty much alert for EVERYONE since they have no previous rank, so you might want to do this offstream. 

If you'd like to add additional commands or processes then, currently, your best bet would be to alter the `lib/ankhbot_clint.rb`. The basic_parse method would be the best place for adding commands which respond to user input, while the `run` method is the best place for adding commands which should be run in a thread or on a timer. 

Ideally we'll chop this type of stuff out into helper files that can be included at runtime so people can share new functionality or add stuff just for themselves without breaking the main client. Haven't had time to do this yet, though, so if you're interested feel free to contribute below. 

### Contributing

I'd love it if you'd like to help out making this thing better or if you just have some cool commands you'd like to add in. Simply fork the repo and submit a PR and I'll be glad to take a look at it. Also feel free to reach out to me with any questions and check out the [Ankhbot Discord](https://discord.gg/J4QMG5m)
