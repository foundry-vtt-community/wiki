Given the vast amount of information out there about ES6 modules it's easy as someone new to JS to get lost trying to figure out how to carry out the simple task of importing a .js library into Foundry, and because the process is simple it is something often overlooked in installation explanations.

### How do I add a third party .js plugin or library so that I can call it inside my character sheet?
Foundry supports ES6 Modules, so the simplest way to import your .js file is to establish an export for it. 

Using Example (example.min.js) constructor class,

> 1. Prepare your .js as an export class.
> a. Open your example.min.js (note: if your .js already begins with "export class" skip step B.)
> b. Wrap the entire .js in "export class <classname> {AllTheFunctionsGoHere}" 

> 2. Define your import
> a. Open your primary modules file (the one defined as "Modules": in your system.json),
> b. at the top you will see something that looks like:

>         // Import Modules
>         import { classname } from "./module/yourclasshere.js"

> c.follow this formatting to import your class. Save.

> 3. Your JS file is now imported! 

### But how do I use it in the HTML for my character sheet? 

Any script you would add as <script> in your HTML file you can add in the extended Actorsheet .js (by using the function 

> activateListeners(html)
>  {
> your script here
> }

