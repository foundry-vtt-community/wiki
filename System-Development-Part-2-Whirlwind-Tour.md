
# Part 2 - Whirlwind Tour



![](https://lh5.googleusercontent.com/FE7hBqyDIAM_Tllj81HK-9i3ONNAKuYJ4tuP9lAtA1srCabeJrhmByZQZ2GYA0KhHiPNWZ_7riOAwWPPPra8vyC3VQ5nC2qs2-iRcO7ucQ_LKjaSqV2uSshEMwrhIan24KfWxDvZ)

  

Before we get ahead of ourselves, we’ll detour very briefly just to survey what exactly we’re about to catastrophically destroy in our attempts to create a working system. These are the files we’re primarily going to be working in:

  

**./template.json**

The template.json contains the data  structure that Foundry automatically applies whenever an entity is created. An entity as far as we’re concerned is just a character or item that needs to have a sheet (form) containing some kind of data. Foundry has other types of entities, but we only care about characters and items.

  

**./styles/simple.css**

The main css file that controls the appearance of everything in our system. We’re mostly interested in this for dealing with making our html pages look pretty.

  

**./templates/actor-sheet.html**

Whenever Foundry creates a character for our system, it uses this page. This is where we’re going to make our character sheet and abuse it into using the data we want it to.

  

**./modules/actor-sheet.js**

The JavaScript “ActorSheet” class for our system. Big and scary. We won’t be spending a lot of time with it.

  

**./templates/item-sheet.html**

The same as actor-sheet.html but for items. We won’t be editing this in this guide.

**./modules/item-sheet.js**

The same as actor-sheet.js… but for items. You get the picture.