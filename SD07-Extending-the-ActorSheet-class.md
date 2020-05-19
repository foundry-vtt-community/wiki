The ActorSheet class is the class associated with our actor's character sheets. Let's take a look at what Boilerplate System does:

## defaultOptions()

Every sheet needs to define its default options.

<!--- {% raw %} --->

```js
/**
 * Extend the basic ActorSheet with some very simple modifications
 * @extends {ActorSheet}
 */
export class BoilerplateActorSheet extends ActorSheet {

  /** @override */
  static get defaultOptions() {
    return mergeObject(super.defaultOptions, {
      classes: ["boilerplate", "sheet", "actor"],
      template: "systems/boilerplate/templates/actor/actor-sheet.html",
      width: 600,
      height: 600,
      tabs: [{ navSelector: ".sheet-tabs", contentSelector: ".sheet-body", initial: "description" }]
    });
  }
```

<!--- {% endraw %} --->

First, we're exporting the class (don't forget to rename yours!) and defining the default options for the sheet. In the <!-- {% raw %} -->`defaultOptions()`<!-- {% endraw %} --> method we need to return a mergedObject of the default options from the main ActorSheet class and our customizations. Those customizations are:

-  **classes**: an array of CSS classes to apply to the character sheet.
* **template**: the path to the Handlebars HTML template that we'll use for this character sheet. This needs to be relative to Foundry's root, so you need to include <!-- {% raw %} -->`systems/MYSYSTEMNAME`<!-- {% endraw %} --> in the start of the path.
* **width**: default window width
* **height**: default window height
* **tabs**: Use this to define your tabs on the character sheet. This should match up with what you've created in your HTML template, but you must have a nav selector CSS class, content selector CSS class, and choose a default/initial tab.

## getData()

Much like the Actor class' <!-- {% raw %} -->`prepareData()`<!-- {% endraw %} --> method, we can use the <!-- {% raw %} -->`getData()`<!-- {% endraw %} --> method to derive new data for the character sheet. The main difference is that values created here will only be available within this class and on the character sheet's HTML template. If you were to use your browser's inspector to take a look at an actor's available data, you wouldn't see these values in the list, unlike those created in prepareData().

<!--- {% raw %} --->

```js
  /* -------------------------------------------- */

  /** @override */
  getData() {
    const data = super.getData();
    data.dtypes = ["String", "Number", "Boolean"];
    for (let attr of Object.values(data.data.attributes)) {
      attr.isCheckbox = attr.dtype === "Boolean";
    }
    return data;
  }
```

<!--- {% endraw %} --->

There's not a whole lot happening in this example of getData(), as we're just checking to see what kind of attribute this is and setting the type to Boolean if it's a checkbox. You may not need to use this, so feel free to skip over it if you have everything you need from the prepareData() method instead.

## activateListeners()

If you want your sheet to be interactive, this is where that needs to happen. The <!-- {% raw %} -->`activateListeners()`<!-- {% endraw %} --> method is where you can execute jQuery on your sheet to do things like create rollable skills and powers, add new items, or delete items. This method is passed an <!-- {% raw %} -->`html`<!-- {% endraw %} --> object that behaves much like <!-- {% raw %} -->`$('.sheet')`<!-- {% endraw %} --> would if you were trying to run jQuery logic on your sheet in your browser's console.

<!--- {% raw %} --->

```js
  /** @override */
  activateListeners(html) {
    super.activateListeners(html);

    // Everything below here is only needed if the sheet is editable
    if (!this.options.editable) return;

    // Add Inventory Item
    html.find('.item-create').click(this._onItemCreate.bind(this));

    // Update Inventory Item
    html.find('.item-edit').click(ev => {
      const li = $(ev.currentTarget).parents(".item");
      const item = this.actor.getOwnedItem(li.data("itemId"));
      item.sheet.render(true);
    });

    // Delete Inventory Item
    html.find('.item-delete').click(ev => {
      const li = $(ev.currentTarget).parents(".item");
      this.actor.deleteOwnedItem(li.data("itemId"));
      li.slideUp(200, () => this.render(false));
    });
  }
```

<!--- {% endraw %} --->

The Boilerplate System includes three examples of click listeners, one to create new items, one to edit existing items, and one to delete items. We'll revisit this later in the tutorial to add a listener for rollable attributes.

The first click listener we added was to create new items, but notice that it uses <!-- {% raw %} -->`this._onItemCreate.bind(this)`<!-- {% endraw %} --> rather than calling its code directly like the edit and delete listeners do. You can follow that code pattern to break your listeners into custom methods to make your code more organized as it grows over time. For now, let's take a closer look at the <!-- {% raw %} -->`_onItemCreate()`<!-- {% endraw %} --> custom method:

<!--- {% raw %} --->

```js
  /* -------------------------------------------- */

  /**
   * Handle creating a new Owned Item for the actor using initial data defined in the HTML dataset
   * @param {Event} event   The originating click event
   * @private
   */
  _onItemCreate(event) {
    event.preventDefault();
    const header = event.currentTarget;
    // Get the type of item to create.
    const type = header.dataset.type;
    // Grab any data associated with this control.
    const data = duplicate(header.dataset);
    // Initialize a default name.
    const name = <!-- {% raw %} -->`New ${type.capitalize()}`;
    // Prepare the item object.
    const itemData = {
      name: name,
      type: type,
      data: data
    };
    // Remove the type from the dataset since it's in the itemData.type prop.
    delete itemData.data["type"];

    // Finally, create the item!
    return this.actor.createOwnedItem(itemData);
  }
```

<!--- {% endraw %} --->

We're doing a few different things here. First, we're getting the element (header) that was clicked, and then we're finding out what type of item it was. In this case that type is <!-- {% raw %} -->`item`, but it could also be something like <!-- {% raw %} -->`feature`<!-- {% endraw %} --> or <!-- {% raw %} -->`spell`<!-- {% endraw %} -->.  After that, we're grabbing any custom data attributes on the element that was clicked and using them to create a new <!-- {% raw %} -->`itemData`<!-- {% endraw %} --> object. Finally, we're passing all of that over to <!-- {% raw %} -->`this.actor.createdOwnedItem(itemData)`<!-- {% endraw %} --> to create the item on this actor.

And since these examples have all been the individual sections, don't forget your closing bracket for the class itself!

<!--- {% raw %} --->

```js
}
```

<!--- {% endraw %} --->

---

* **Prev:** [Extending the Actor class](https://foundry-vtt-community.github.io/wiki/SD06-Extending-the-Actor-class)
* **Next:** [Creating HTML templates for your actor sheets](https://foundry-vtt-community.github.io/wiki/SD08-Creating-HTML-templates-for-your-actor-sheets)