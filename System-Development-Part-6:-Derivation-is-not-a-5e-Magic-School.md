
![](https://lh6.googleusercontent.com/1UfbCbWz54rZXds2llYZn0ebmut4mSwjCdqwpkHoJf4LIex2pdeE1Ao24vR1z9S4O3n7-uatgsmN5oBKaQZrdt9qnKH5rCYICBYpew1abnkZn52H4EPZRkcN4XBE6Uhhsex-gKp4)

# Optional  

One of the things that most often seems to cause difficulty for potential system developers is calculating derived values; numbers on the character sheet that are the sum of some other values.

  

Usually, it’s because it involves JavaScript, and Simple Worldbuilding System isn’t pre-packaged and ready to do it.

  

This guide will take you through every step of the process, giving you some rudimentary JavaScript necessary to calculate values, and will explain why each step is being done.

  

***You do not need to know anything about JavaScript to do this.***

  

Keep to the following rules when editing any .js file for this procedure and you should not have any issues.

1.  Case is important.
    
2.  Punctuation is important.
    
3.  Brackets and curly braces must always be closed.
    
4.  Consistency is important, names are (mostly) not.
    

  

Let’s suppose for example we have a **defense** stat we need to calculate.

  

We know that **defense = agility+dodge**.

  

We could leave this to the players, and have them write a number in an input box we created to catch the **defense** value. Yet are we not *benevolent* GMs? Let’s make the computer do it for them instead.

## 6a. Create a value to be derived

From our example, we’ll create an entry in our template.json to catch defense.

    "derived": {
    
    "defense": {
    
    "value": 0,
    
    "label": "Defense",
    
    "modifier": []
    
    }
    
    }
    
      

(if you do not have two or more other stats to add together, now would be a good time to add them as well. Don’t forget to restart Foundry after editing the template.json, and create a new actor.)

  

## 6b. Creating an Actor Class extension

  

Create a new file in your **./modules/** directory, it can be called anything you like as long as you remember it and it ends in .js , so “**myactorclass.js**”

  

**Why do we need an Actor class file?**

The most convenient way to handle derived values needs a particular JavaScript function (a piece of code that JavaScript runs to do something) called *prepareData()*. The *prepareData()* function in Foundry is run by “**Actor**” not “**ActorSheet**”. Simple Worldbuilding System does not come with an “**Actor**” class file, so we *have to make our own.*

  

## 6c. Create some important code in the Actor class file

  

Our actor class needs to contain the following JavaScript for it to work with Foundry:

  

Replace “MySystem” in ActorMySystem with whatever you want, as long as you follow that capitalization pattern for consistency.

    export  class  ActorMySystem  extends  Actor {
    
    prepareData() {
    
    super.prepareData();
    
    const  actorData = this.data;
    
    const  data = actorData.data;  
    if (actorData.type === "character") {
    
    data.defense.value = Number(attr.agility.value)+Number(attr.dodge.value);
    
    }
    
      

What this code does is:  
  

-   Tells JavaScript this is a class to be exported (used in another file)
    
-   That it “extends” a bit of code that exists in Foundry
    
-   That it contains a function called **prepareData(),** which contains some code that we want Foundry to do when it runs **prepareData()** normally
    
-   That we still want it to run **prepareData()** from Foundry itself (**super.prepareData()**)
    
-   Then it establishes two **constants** which we will use to make our lives easier
    
-   Finally it establishes an ‘**if**’ clause, telling Foundry we only want to do these things on actors that are characters
    

  

Once you have that entered and saved, we’ll ***keep this file open*** for a future step but we have one more thing to do before we can start deriving values.

  

## 6d. Create some important code in the main Javascript file for your system

  

In **./modules/simple.js**

  

**Before**

    // Import Modules
    
    import { SimpleItemSheet } from  "./item-sheet.js";
    
    import { SimpleActorSheet } from  "./actor-sheet.js";
    
    /* -------------------------------------------- */
    
    /* Foundry VTT Initialization */
    
    /* -------------------------------------------- */

  

**After**

    // Import Modules
    
    import { SimpleItemSheet } from  "./item-sheet.js";
    
    import { ActorMySystem } from  "./myactorclass.js";
    
    import { SimpleActorSheet } from  "./actor-sheet.js";
    
    /* -------------------------------------------- */
    
    /* Foundry VTT Initialization */
    
    /* -------------------------------------------- */
    
      

What this code does is:  
  

-   Tells JavaScript to import our newly created **ActorClass** from the .js file we created
    

  
  
  

## 6e. Derive a value

  

Back in our **ActorClass**, we’re going to add a very, very rudimentary calculation to our sheet.

  
Since we know that **defense = agility+dodge** we are going to tell Foundry that.

  

    export  class  ActorMySystem  extends  Actor {
    
    prepareData() {
    
    super.prepareData();
    
    const  actorData = this.data;
    
    const  data = actorData.data;  
    if (actorData.type === "character") {
    
    data.derived.defense.value = Number(attr.agility.value)+Number(attr.dodge.value);
    
    }

  

What this code does is:  
  

-   Tells Foundry that the **value** of **data.derived.defense** is equal to the **sum** of the **object values** for **agility** and **dodge**, and that those values are to be considered **numbers** (even if they aren’t entered in the data as numbers)
    

  

While wrapping the values in **Number** is not actually necessary here, it does work to solve the occasion that someone puts a text string in the box for either agility or dodge. In those cases you will see “NaN” in place of anywhere you used **data.defense.value**.

  

## 6f. Use your new derived on the character sheet

  

In any div on your character sheet’s HTML, add the following:

  

    Testing our Defense Derived: {{data.derived.defense.value}}
    
      

If it worked, when you refresh your sheet, and you should see “Testing Our Defense Derived:” If the value is 0, it **very likely** won’t appear on your character sheet as anything but that. So let’s change our Agility score to a number. After it changes, the value should appear after our “...Derived:”

  

Once it appears, change the value in the skills box. If it worked correctly, **defense** should always be equal to **agility+dodge**.

  

That’s it. You now know how to have your sheet use derived values of any kind.