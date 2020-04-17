![](https://lh5.googleusercontent.com/Jbky61hs2_yrsXWmf7T5dve6BR7Xh9IeukK60zOHZdQjQd7dWAIvSBmwEvND7hVWRiXDfGyL8AWzJ67Xhn5n1mg2GDXCDbFLrsluzRNntUF2wa_msKcGyPlzPtqEmmRwOq2BPVIY)

  
  

Now that we know Foundry can see our system and we’ve got a development world created, we can start the preliminaries of building our character sheet. It is best to do these steps with a copy of a character sheet for your system in front of you, so if you’re planning on making Paranoia, best get your clone sheet ready.

  

## 3a. Open both the template.json and the ./templates/actor-sheet.html files in your editor.

(in VSCode you can conveniently right click one of these files at the top of the screen after opening it and choose ‘split right’ for a split-screen view.)

![](https://lh3.googleusercontent.com/IUym1frwBawJe8KKZferP2Bq26is2DkHeCJCzl6VX4KOn8eOoBYN6I_rxqgS6XEvEpsxx-GjJkNKgfWNzODljXrCNHL5_y_HKTz0zNyLYmCc0ispIudkU4tmXpC7GS2E861X6bAh)

  

The window on the left is our template.json file containing all our data-to-be-used, the window on our right is an html file that uses that data.

  
  

## 3b. Read and understand some HTML

Some of you will already be able to piece together what’s happening here, but for the sake of thoroughness, we’ll look closer at lines 7, 9, and 11 in our html file.

7:

    <h1  class="charname"><input  name="name"  type="text"  value="{{actor.name}}"  placeholder="Name"/></h1>

9:

    <input  type="text"  name="data.health.value"  value="{{data.health.value}}"  data-dtype="Number"/>

11:

    <input  type="text"  name="data.health.max"  value="{{data.health.max}}"  data-dtype="Number"/>

  

Each of these lines creates an <input> text box on our character sheet, and each one is linked to something different. Greatly simplified: whenever Foundry makes a character, it creates a database object for that character called actor and gives actor a sub-entry called data that contains everything from our template.json file that we told it an actor needs.

  

Foundry comes with some predefined Handlebars. These are effectively shortcuts we can use that tell Foundry to read {{data.health.value}} from data related to the actor.

  

In short: whenever you see something wrapped in {{}} in html for Foundry, it’s a shortcut that (likely) references some data from a JSON object.

  

We can use this exact structure to make our own entries. Name always refers to the path to where we want our data  stored. Value always refers to the actual information we’re storing.

  
So if our maximum health is 10, that information is stored at “data.health.max”, which in our template looks like this:

![](https://lh6.googleusercontent.com/P5sMHzvXu3oNJlKnu7J17dSp0BPRSzrLyOx0sAKtr-XxXvBo7ZRUUfiHjAHRDBVZN01JT-ED_H7jRmVDzunuzEuwxbxVFPadvnyCf6OIjK9YltorCBf9QZg1H3WjcQY6QW2Yn2Dt)

But we don’t get the value to show up in the box unless we tell Foundry to give us the value using {{data.health.max}}.

  

**Name** tells Foundry where to store the information.

**Value** tells Foundry to get the information for us.

  
  
  
  

## 3c. Break Everything

Now that we can see how foundry references our data, let’s give it some data to reference. The “Actor” section of our template.json contains only one type, which suits us just fine. We only care about characters and only really want to make a character sheet anyway.

  

We don’t plan on using the freeform attributes system from foundry, so let’s get rid of that.

  
  

Before

![](https://lh4.googleusercontent.com/blH3H9pcrFUH8ujy704w-WJcmY_mk3JawJjCoL8FfRXlgjPTzt7GWC2Ev88-FeqUfKDwjTkauppyPt2noBadKvAt0ixNw8Qo0rR80vfO-x4AWTKOAYM3ZNA16of45Ok087EGEUkJ)

  

After

![](https://lh6.googleusercontent.com/KJCYcNfvl859zAsV93ds5Ss3sDDdFh8i8e7YwCqJGjsqUUzrVmqTd1qPyStHEKevP2n__mIzJmnA2hA3QR5ocmAcDISx1HNPXblr6pRQdC1hsXQCRnuoUhy_hpcrtXquILxStd_H)  

But, since we have a bunch of stuff that references that data, we need to make sure that we’re not just getting rid of it in the data but the HTML as well. If we don’t, we won’t be able to open the character sheet because of errors telling us that Foundry can’t find some data it was told to look for.

  

So in our **actor-sheet.html** we’ll just heartlessly delete the really nice free-form attributes system that Atropos made for us so we can put in our own boring text input boxes.

  

Before

![](https://lh6.googleusercontent.com/RdZ_g2Zs8BqUMl_o7DhN9s8eduTJHS_SYvLy8YuH57Gqf680SMCFrLBkrqt-dMjQz_LU_GTKtS6pZfFbvBTe09dhZtlE43329RMpTC4HK6IUjPsXdGL4eYJN2YcitVFWdzuQZP6F)

After

![](https://lh4.googleusercontent.com/nv412l_e78SC9Sk2hgaLPIGe-q6tfFlCeYK_kFKMesfMqVzOxoDMj5bvBEO4sahqTXuK-FsO_fY2qx_gTXDp1AjdpReV4HyTo7_FoBI6DNu86SVLItGLj0GwCTwojDXRRrUxqaOt)

  

(yes, we could remove the header from the attributes tab as well if we wanted to.)

  
  
  

But we’re still getting the same error.

  

![](https://lh6.googleusercontent.com/CdD6Uj7LFeyATZvrU7dfVHox___beacZPBeQkBspVwvmcJ5wf_uR_hyTzC35UPObrLqRykloCTKhe6rBQhM499_cG4DMPbHWhLbP6fD-iEIIHab4a1mMv7yUnC5zl70GNMvshD98)

  

Woops.

  

Looks like we forgot to tell Javascript not to do something with the attributes page. Fortunately this tells us right away what it’s doing, and where to go look for it: actor-sheet.js:24 is the file and the line number. So let’s go make up for our wholesale butchery of the code with more wholesale butchery.

  

## 3d. Prepare to fix everything

Open **./module/actor-sheet.js** and take a minute to convince yourself that JavaScript isn’t overwhelming and that you won’t immediately break everything in existence by editing this file.

  

Now we’re going to delete chunks out of this file arbitrarily until our character sheet works again.

## 3e. There can’t be a problem in the code if we delete the code

Let’s start with anything referencing attributes. Inside this function, there’s a little bit of code that reads each one of our data.attributes and turns anything that’s a checkbox into a boolean… whatever the hell that is. Let’s get rid of that.

  
Before

    getData() {
    
    const  data = super.getData();
    
    data.dtypes = ["String", "Number", "Boolean"];
    
    for ( let  attr  of  Object.values(data.data.attributes) ) {
    
    attr.isCheckbox = attr.dtype === "Boolean";
    
    }
    
    return  data;
    
    }

  

After

  

    getData() {
    
    const  data = super.getData();
    
    data.dtypes = ["String", "Number", "Boolean"];
    
    return  data;
    
    }

  
  

But wait, we’re not done here. Near the bottom of this page is a whole bunch of code that Atropos kindly slaved to produce. It does stuff like: listen for when we click a button to create new attributes, delete attributes that we don’t want anymore, and update our actor when we do either of those two things. Since we don’t have those buttons anymore, let’s just delete 30% of the JavaScript that we have left in this file.

  

Starting from the lines that reads:

    // Add or Remove Attribute
    
    html.find(".attributes").on("click", ".attribute-control", this._onClickAttributeControl.bind(this));
    
    }
    
      

Delete everything except the very last } in the file, and then add one more } so that we have the right number of curly braces left.

  

  
The last lines in our actor-sheet.js should now read:

![](https://lh5.googleusercontent.com/hdI-wC2DwGs2GMjekWUKntWB3hS_dMNMl2YUsL5pXAOuHaq7WKBIjfKBs1xic-PmidSV50YN2U0B-jeVB4w-21kstZvKu0aMpziOtW1VI2siVHmD04nZXJsUl4s2-v2E7usPI0_V)

  

## 3f. One last thing

While we’re in here, the character sheet is still pointing at the worldbuilding system. So let’s fix that real quick.

Before

    classes: ["worldbuilding", "sheet", "actor"],
    
    template:  "systems/worldbuilding/templates/actor-sheet.html",
    
    width:  600,
    
    height:  600,
    
    tabs: [{navSelector:  ".sheet-tabs", contentSelector:  ".sheet-body", initial:  "description"}]
    
      

After

    classes: ["worldbuilding", "sheet", "actor"],
    
    template:  "systems/yoursystemname/templates/actor-sheet.html",
    
    width:  600,
    
    height:  600,
    
    tabs: [{navSelector:  ".sheet-tabs", contentSelector:  ".sheet-body", initial:  "description"}]
    
      

  

Now that we’ve given the Simple Worldbuilding System a bit of a lobotomy, we can get back to creating our sheet.



