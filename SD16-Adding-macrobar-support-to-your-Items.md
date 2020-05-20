## Update your main system JS

First, we need to update your <!-- {% raw %} -->`game.mysystemname`<!-- {% endraw %} --> object in your init hook. For the Boilerplate System, that looks like this:

<!--- {% raw %} --->

```js
game.boilerplate = {
  BoilerplateActor,
  BoilerplateItem,
  rollItemMacro
};
```

<!--- {% endraw %} --->

The only change we've made from earlier is that we've added a new line for <!-- {% raw %} -->`rollItemMacro`<!-- {% endraw %} -->, which we'll define later.

Next we need to create (or modify) your ready hook in the main system JS file for your system. For the Boilerplate System, that's <!-- {% raw %} -->`boilerplate.js`

<!--- {% raw %} --->

```js
Hooks.once("ready", async function() {
  // Wait to register hotbar drop hook on ready so that modules could register earlier if they want to
  Hooks.on("hotbarDrop", (bar, data, slot) => createBoilerplateMacro(data, slot));
});
```

<!--- {% endraw %} --->

Next we'll need to add two new functions to both add the drop behavior and the roll function. Place the following after (not inside) your ready hook. Rename the <!-- {% raw %} -->`createBoilerplateMacro`<!-- {% endraw %} --> function both here and in the ready hook above to be more appropriate to your system, such as <!-- {% raw %} -->`createMySystemNameMacro`

<!--- {% raw %} --->

```js
/* -------------------------------------------- */
/*  Hotbar Macros                               */
/* -------------------------------------------- */

/**
 * Create a Macro from an Item drop.
 * Get an existing item macro if one exists, otherwise create a new one.
 * @param {Object} data     The dropped data
 * @param {number} slot     The hotbar slot to use
 * @returns {Promise}
 */
async function createBoilerplateMacro(data, slot) {
  if (data.type !== "Item") return;
  if (!("data" in data)) return ui.notifications.warn("You can only create macro buttons for owned Items");
  const item = data.data;

  // Create the macro command
  const command = `game.boilerplate.rollItemMacro("${item.name}");`;
  let macro = game.macros.entities.find(m => (m.name === item.name) && (m.command === command));
  if (!macro) {
    macro = await Macro.create({
      name: item.name,
      type: "script",
      img: item.img,
      command: command,
      flags: { "boilerplate.itemMacro": true }
    });
  }
  game.user.assignHotbarMacro(macro, slot);
  return false;
}

/**
 * Create a Macro from an Item drop.
 * Get an existing item macro if one exists, otherwise create a new one.
 * @param {string} itemName
 * @return {Promise}
 */
function rollItemMacro(itemName) {
  const speaker = ChatMessage.getSpeaker();
  let actor;
  if (speaker.token) actor = game.actors.tokens[speaker.token];
  if (!actor) actor = game.actors.get(speaker.actor);
  const item = actor ? actor.items.find(i => i.name === itemName) : null;
  if (!item) return ui.notifications.warn(`Your controlled Actor does not have an item named ${itemName}`);

  // Trigger the item roll
  return item.roll();
}
```

<!--- {% endraw %} --->

The first function is used to create a new macro entity on drop and set its command to <!-- {% raw %} -->`game.boilerplate.rollItemMacro(ITEMNAME)`<!-- {% endraw %} -->, and the second function is the actual function that will trigger the roll on the item. Rename <!-- {% raw %} -->`boilerplate`<!-- {% endraw %} --> in that command to whatever your system's namespace is. This namespace is for the same object we created in the first step of this tutorial, so it should match that.

The last line of the <!-- {% raw %} -->`rollItemMacro()`<!-- {% endraw %} --> function is to call <!-- {% raw %} -->`item.roll()`<!-- {% endraw %} -->. So let's switch over to your <!-- {% raw %} -->`Item`<!-- {% endraw %} --> class and add that method.

## Adding <!-- {% raw %} -->`roll()`<!-- {% endraw %} --> to the Item class

The <!-- {% raw %} -->`roll()`<!-- {% endraw %} --> method is what we're calling when the macro is clicked, so you can put any logic into this. Here's an example from the Boilerplate System, but you should modify this to fit your needs.

<!--- {% raw %} --->

```js
/**
 * Handle clickable rolls.
 * @param {Event} event   The originating click event
 * @private
 */
async roll() {
  // Basic template rendering data
  const token = this.actor.token;
  const item = this.data;
  const actorData = this.actor ? this.actor.data.data : {};
  const itemData = item.data;

  // Define the roll formula.
  let roll = new Roll('d20+@abilities.str.mod', actorData);
  let label = `Rolling ${item.name}`;
  // Roll and send to chat.
  roll.roll().toMessage({
    speaker: ChatMessage.getSpeaker({ actor: this.actor }),
    flavor: label
  });
}
```

<!--- {% endraw %} --->

We're almost done! The last thing we have to do is make sure your character sheet has the proper drag events to be able to drag to the macrobar.

## Add drag events to the ActorSheet class

In your <!-- {% raw %} -->`activeListeners()`<!-- {% endraw %} --> method, add the following code.

<!--- {% raw %} --->

```js
// Drag events for macros.
if (this.actor.owner) {
  let handler = ev => this._onDragItemStart(ev);
  // Find all items on the character sheet.
  html.find('li.item').each((i, li) => {
    // Ignore for the header row.
    if (li.classList.contains("item-header")) return;
    // Add draggable attribute and dragstart listener.
    li.setAttribute("draggable", true);
    li.addEventListener("dragstart", handler, false);
  });
}
```

<!--- {% endraw %} --->

If this is the actor's owner, we're going through all <!-- {% raw %} -->`<li>`<!-- {% endraw %} --> tags with the <!-- {% raw %} -->`<!-- {% endraw %} -->.item`<!-- {% endraw %} --> class, ignoring those with the <!-- {% raw %} -->`<!-- {% endraw %} -->.item-header`<!-- {% endraw %} --> class. You should update those two selectors to match what your system actually uses if they're different. Once we're inside the loop we add the <!-- {% raw %} -->`draggable`<!-- {% endraw %} --> attribute and <!-- {% raw %} -->`dragstart`<!-- {% endraw %} --> event to the list item to make it draggable for macrobar support. This will also allow you to do other things with the drag event, but that's outside of the scope of this part of the tutorial.

---

* **Prev:** [Separating item types into tabs](https://foundry-vtt-community.github.io/wiki/SD11.4-Separating-item-types-into-tabs)
* **Next:** To be continued...