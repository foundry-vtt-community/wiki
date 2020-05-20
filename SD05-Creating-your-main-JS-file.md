Let's take a look at the Boilerplate System's <!-- {% raw %} -->`/module/boilerplate.js`<!-- {% endraw %} --> file. We'll look at each section of it to see what's happening:

## Import your classes
<!--- {% raw %} --->

```js
// Import Modules
import { BoilerplateActor } from "./actor/actor.js";
import { BoilerplateActorSheet } from "./actor/actor-sheet.js";
import { BoilerplateItem } from "./item/item.js";
import { BoilerplateItemSheet } from "./item/item-sheet.js";
```

<!--- {% endraw %} --->

In this first section, we've imported 4 classes, one each for the Actor and Item classes, and one each for the ActorSheet and ItemSheet classes. For this system, those classes have <!-- {% raw %} -->`Boilerplate`<!-- {% endraw %} --> as a prefix for them, but you should use a name more appropriate to your system when creating your own. The code for them is defined in <!-- {% raw %} -->`/module/actor`<!-- {% endraw %} --> and <!-- {% raw %} -->`/module/item`<!-- {% endraw %} -->, so we have to reference their file locations when importing.

Importing doesn't necessarily do anything at this point, but we do have the classes available in our file so that we can now let Foundry know how to use them.

## The 'init' hook

Foundry has a very robust hooks system that lets you hook into different kinds of events, such as <!-- {% raw %} -->`init`<!-- {% endraw %} -->, <!-- {% raw %} -->`ready`<!-- {% endraw %} -->, or other hooks for chat messages, scene render, etc. In this case, we'll be using the <!-- {% raw %} -->`init`<!-- {% endraw %} --> hook to initialize the important overrides in our system. In the example below, everything with the exception of registering the Handlebars helpers should be considered essential for your system's init hook.

This example includes comments behind <!-- {% raw %} -->`//`<!-- {% endraw %} --> that explain more about what's actually happening.

<!--- {% raw %} --->

```js
Hooks.once('init', async function() {

  // Place our classes in their own namespace for later reference.
  game.boilerplate = {
    BoilerplateActor,
    BoilerplateItem
  };

  /**
   * Set an initiative formula for the system
   * @type {String}
   */
  CONFIG.Combat.initiative = {
    formula: "1d20",
    decimals: 2
  };

  // Define custom Entity classes. This will override the default Actor and
  // Item classes to instead use our extended versions.
  CONFIG.Actor.entityClass = BoilerplateActor;
  CONFIG.Item.entityClass = BoilerplateItem;

  // Register sheet application classes. This will stop using the core sheets and
  // instead use our customized versions.
  Actors.unregisterSheet("core", ActorSheet);
  Actors.registerSheet("boilerplate", BoilerplateActorSheet, { makeDefault: true });
  Items.unregisterSheet("core", ItemSheet);
  Items.registerSheet("boilerplate", BoilerplateItemSheet, { makeDefault: true });

  // If you need to add Handlebars helpers, here are a few useful examples:
  Handlebars.registerHelper('concat', function() {
    var outStr = '';
    for (var arg in arguments) {
      if (typeof arguments[arg] != 'object') {
        outStr += arguments[arg];
      }
    }
    return outStr;
  });

  Handlebars.registerHelper('toLowerCase', function(str) {
    return str.toLowerCase();
  });
});
```

<!--- {% endraw %} --->

And that's it!

## Making it your own

As with previous examples, this sample code using the Boilerplate System. You should rename your classes such as <!-- {% raw %} -->`MySystemNameActor`<!-- {% endraw %} --> instead of <!-- {% raw %} -->`BoilerplateActor`<!-- {% endraw %} -->, and you'll want to update the <!-- {% raw %} -->`registerSheet()`<!-- {% endraw %} --> lines to replace <!-- {% raw %} -->`boilerplate`<!-- {% endraw %} --> with <!-- {% raw %} -->`mysystemname`<!-- {% endraw %} -->, using your system's machine name.

Now let's take a look at the extended Actor class.

---

* **Prev:** [template.json](https://foundry-vtt-community.github.io/wiki/SD04-template.json)
* **Next:** [Extending the Actor class](https://foundry-vtt-community.github.io/wiki/SD06-Extending-the-Actor-class)