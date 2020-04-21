![](https://lh5.googleusercontent.com/KR7cbbOgyDCzOwHYMYI4J0rHHEamSIAD8IPTfwNoo7ezzgZ_R4m_RciTrz5nA7SHrgafl0B94PyY6EvN8iDMgQTB1HW66hXguch2cWMz9J4miyKjDF7Gx78-ehepBJiP8h5iK4cz)
  
  

From here on the majority of our work is going to be editing html and css. You can keep the template.json folder open and use that to remember the structure of your data, if you get lost, remember that everything contained within the “character”: {} JSON is what Foundry sees as “data.<something>”

  

The same is also true for items, but we’re not editing an item sheet in the scope of this guide (it is a wholly identical process, however).

  

Each of these steps will demonstrate the syntax for how to add various things to your sheet.

  

## 5a. Create an input text box for an attribute/skill, individually
This HTML tag is the most basic way to accept input and have it stored in the data on the actor.
  

    <label  class="attribute-label"> Strength: </label>
    
    <input  type="text"  name="data.attributes.strength.value"  value="{{data.attributes.strength.value}}"  data-dtype="Number"/>
    
      

## 5b. Create input boxes for all attributes, programmatically using a {{Handlebars}} helper
Use this if you have a lot of attributes and you want to automatically populate them with input boxes. Slightly more difficult.

    <ol  class="attributes-list">
    
    {{#each actor.data.attributes as |attrib key|}}
    
    <li  class="attribute flexrow"  data-attribute="{{key}}">
    
    <span  class="attribute-label flexrow"  name="data.attributes.{{key}}.label">{{label}}</span>
    
    <div  class="attribute-editbox flexrow">
    
    <input  class="attribute-value"  type="text"  name="data.attributes.{{key}}.value"  value="{{attrib.value}}"  data-dtype="Number"  />
    
    </div>  
    </li>
    
    {{/each}}
    
    </ol>
    
      

This establishes an ordered list, then calls the {{#each}} helper. The each helper iterates everything in a list of objects from our data and does something for every object that list contains. So in this case, for every item in our attributes object {data.attributes} it creates a list item `<li>` that contains a `<span>` and the {{label}} of that attribute, and then creates an `<input>` text box for that attribute that is linked to the JSON data.

  

To adapt it for something like skills, it could look like

    {{#each actor.data.skills as |skill key|}}

And then you would change out any reference to attributes to read “skills” and any reference to attrib to read “skill”.

  

## 5c. Create a new tab or rearrange the navigation menu

  

Find the navigation menu, it looks like this:

    {{!-- Sheet Tab Navigation --}}
    
    <nav  class="sheet-tabs tabs"  data-group="primary">
    //a bunch of <a> tags
    </nav>
    
      

Add a new line before the `</nav>` that reads:

    <a  class="item"  data-tab="yourtabnamehere">Your Tab Name Here</a>

  

Put it wherever you want it in the order of navigation.  
  
Then add a new section for yourself to work in. anywhere within the `<section class=”sheet-body”></section>`

    {{!-- Your Tab Name Here Tab --}}
    
    <div  class="tab yourtabnamehere"  data-group="primary"  data-tab="yourtabnamehere">
    
      
      

## 5d. Create a checkbox

  

Remember earlier when I joked “whatever that is” about Boolean? To make a checkbox, you need to set a boolean value up in your template.json. It’s way easier than it sounds.

In your template.json. You can set anything to a true or false instead of a 0 in order to turn it into a boolean.

  

First: In your template.json

![](https://lh4.googleusercontent.com/UUW7ueQMKQH8fo91VuekQsgPVhHVzG6kGDN_uI4mEfEglueOAnH__ck5mNrLfljVj7gXUeezdANYJ2Elm1fXY2VEgqTOaOpV03K9-2dFi-F_btQrL2gWRb3h6YUGyuPap3oIoFSf)

  

NOTE: If you change your template.json you need to restart Foundry to see the change (and create a new actor for the data to show up in it).

  
  
  

Then in your HTML:

`    <input  type="checkbox"  name="data.attributes.strength.proficient"  {{checked  actor.data.strength.proficient}}>`

  

## 5e. Text Areas

Creating a text area that Foundry will show users to conveniently edit large blocks of text like a character background or a personal notepad only requires two things: a place to put the data, and use of the handlebars Editor helper.

  
The editor helper stores the data as some conveniently formatted HTML in a text string. So we’ll add an empty text string to our template.json.

    "character": {
    
    "race": {
    
    "value": "",
    
    "label": "Race"
    
    }
    
    "yournotepadhere": "",
    
    "biography": "",
    
      

As always - restart foundry and create a new Actor after changing your template.json.

  

Then we’ll add an editor to our sheet:

    <div  class="ourrandomtexteditor">
    
    {{editor content=data.yournotepadhere target="data.yournotepadhere" button=true owner=owner editable=editable}}
    
    </div>
    
      

Please note: if this data box is empty the editing window may not be big enough to click into. You’ll need to use some css on the “.editor-content” class to set a minimum height to overcome that obstacle.

  

## 5f. Select boxes

A dropdown menu for selecting something from a list, this requires you to define a list of items the same way we did a list of attributes.  
  

It also requires a place to store the information.

  

    In template.json:

    "character": {

        "race": {

            "value": "",

            "label": "Race"

        }

        "biography": "",

        "races": {

            "dwarf": {

                "label": "Dwarf",

                "dtype": "String"

            },

            "elf": {

                "label": "Elf",

                "dtype": "String"

            },

            "gnome": {

                "label": "Gnome",

                "dtype": "String"

            }
        }
    }
    

    
      

In your HTML:

    <select  class="selectrace"  name="data.race.value"  data-type="String">
    
    {{#select actor.data.race.value}}
    
    {{#each actor.data.races as |race key|}}
    
    <option  value="{{key}}">{{race.label}}</option> {{/each}} {{/select}}
    
    </select>




In order, this establishes an html select box. 

Then we use the handlebars helper for select to tell Foundry what, exactly, we're selecting. 

Then the `#each` helper reads all of our available races from actor.data.races and assigns them to a shortcut.

Then we establish some options related to our each class, which determines the value of each potential option and gives it a human-readable label.

