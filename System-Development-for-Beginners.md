
##  The “I Just Want A Custom Character Sheet ASAP” edition

  

This guide is a highly condensed form of a much bigger and more detailed guide still being written. Until it’s done, however, this will serve to:

  

1.  Illustrate the fundamentals of how a Foundry system uses its data
    
2.  Explain the template.json and the ‘handlebars’ functions Foundry uses for its data
    
3.  Teach extremely basic JavaScript for the purposes of deriving values (such as a calculated defensive attribute)
    
4.  Get you to a point where you can use HTML and CSS skills to make your sheet look how you want
    

##### Chapters
* [<a href="System-Development-Part-1-I-Made-This">System Development Part 1: I Made This</a>](system-development-part-1:-i-made-this)
* [<a href="System-Development-Part-2-Whirlwind-Tour">System Development Part 2: Whirlwind Tour</a>](#system-development-part-2-whirlwind-tour)
* [<a href="System-Development-Part-3-Breaking-Everything">System Development Part 3: Breaking Everything</a>](#system-development-part-3-breaking-everything)
* [<a href="System-Development-Part-4-Bureaucracy">System Development Part 4: Bureaucracy</a>](#system-development-part-4-bureaucracy)
* [<a href="System-Development-Part-5-Wandering-in-%23000000">System Development Part 5:Wandering in #000000</a>](#system-development-part-5-wandering-in-%23000000)
* [<a href="System-Development-Part-6-(optional)-Derivation-is-not-a-5e-Magic-School">System Development Part 6 (optional) Derivation is not a 5e Magic School</a>](#system-development-part-6-(optional)-derivation-is-not-a-5e-magic-school)

This guide is designed for people who have at least rudimentary knowledge of HTML and CSS, and are sufficiently capable of reading a piece of Javascript to make an educated guess what it does. Engaging with a coding language may be scary, but Javascript is reasonably friendly to new users.

  

This guide also makes some assumptions:

-   That you know where your FoundryData folder is
    
-   That you know how to work some routine functions in your operating system (such as copying and pasting, renaming files and folders)
    
-   That you have a copy of Visual Studio Code installed (or another IDE of your choosing)
    
-   That you already know how to install a System for Foundry
    
-   That you are doing your development on a local copy of Foundry and not a remote server
    
-   That you are developing this system in a world not used for active play
    

  

## Introduction

One of the most common phrases when a new GM comes to pick up Foundry and is excited about getting their custom system playable is “all I need is my character sheet.”  
  
That was certainly my first thought when I jumped into Foundry development.

  

But a character sheet isn’t just a piece of paper with a bunch of plain text fields on it. At least, not where any virtual tabletop is concerned. Behind that simple piece of paper there are a lot of calculations and secret information that we, as players and GMs, simply do in our heads without considering.

  

A computer can’t do that unless we give it all the details.

  

The character sheet is the point of convergence for nearly every piece of a roleplaying game. It contains all of the rules, distilled to the simplest format. If you’ve made your character sheet, you have made your system.

  
So let’s just build a system.

  
  

## One Last Caveat

If you only have a passing familiarity with Javascript, this guide will  be instructive enough to let you scrape by, but you will likely be subjecting yourself to unnecessary difficulty trying to tackle some things outside its bounds if you plan to continue with developing your system.

  

When I first undertook drafting my system, I was missing a lot of necessary JS knowledge, and in my hubris I thought I’d learn as I went. How hard could it be, right? It wasn’t until several weeks after my system was done that I decided to put myself through a basic Javascript course, and over just the first few hours of that course I learned all of the skills that had taken me days of research and self-study to learn using google searches, trial and error, and a lot of handholding from the Foundry development community.

  

What I’m saying is: learn from my mistake.

  

Before you do anything else, go run yourself through [Codecademy’s Introduction to Javascript](https://www.codecademy.com/learn/introduction-to-javascript). It’s free, and though the course takes about ten hours to complete in entirety, you will come out of it knowing 90% of the things you need to code a system for Foundry. A few hours or a couple of days dedicated to preparing for this task will make your life a lot easier.
