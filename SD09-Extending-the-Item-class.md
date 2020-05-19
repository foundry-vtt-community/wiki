The ItemSheet class is the class associated with our item sheets. Let's take a look at what Boilerplate System does:

## defaultOptions()

Very similar to the actor sheet, we start out by defining our default options for this sheet. Our width and height tend to be smaller on item sheets so that they don't fully cover up the character sheet when they're opened. One thing that we did differently from the actor sheet is that this defaultOptions() method doesn't have a template property. That's intentional, and it could have been done on the actor sheet as well if we needed to. If you don't include a template property, you should create a <!-- {% raw %} -->`template()`<!-- {% endraw %} --> getter method to return the correct template.

<!--- {% raw %} --->

```js
/**
 * Extend the basic ItemSheet with some very simple modifications
 * @extends {ItemSheet}
 */
export class BoilerplateItemSheet extends ItemSheet {

  /** @override */
  static get defaultOptions() {
    return mergeObject(super.defaultOptions, {
      classes: ["boilerplate", "sheet", "item"],
      width: 520,
      height: 480,
      tabs: [{ navSelector: ".sheet-tabs", contentSelector: ".sheet-body", initial: "description" }]
    });
  }
```

<!--- {% endraw %} --->

## get template()

The <!-- {% raw %} -->`template()`<!-- {% endraw %} --> method has the <!-- {% raw %} -->`get`<!-- {% endraw %} --> keyword placed before it to signal that this is a getter method for a property. In this case, we're just returning a single <!-- {% raw %} -->`${path}/item-sheet.html`<!-- {% endraw %} --> template for all items. However, if you have multiple item types such as <!-- {% raw %} -->`item`, <!-- {% raw %} -->`feat`, and <!-- {% raw %} -->`spell`, you could remove the first return statement and uncomment the second return statement to dynamically return a template matching the item type name, such as <!-- {% raw %} -->`templates/item/spell-sheet.html`<!-- {% endraw %} -->.

<!--- {% raw %} --->

```js
  /** @override */
  get template() {
    const path = "systems/boilerplate/templates/item";
    // Return a single sheet for all item types.
    return <!-- {% raw %} -->`${path}/item-sheet.html`;
    // Alternatively, you could use the following return statement to do a
    // unique item sheet by type, like <!-- {% raw %} -->`weapon-sheet.html`<!-- {% endraw %} -->.

    // return <!-- {% raw %} -->`${path}/${this.item.data.type}-sheet.html`;
  }
```

<!--- {% endraw %} --->

## getData()

As with the actor sheet, you can use this to create derived data for your item sheet if needed. Values created here would only be available within this class or on the sheet's HTML template; it would not be available through returning the item entity elsewhere.

<!--- {% raw %} --->

```js
  /* -------------------------------------------- */

  /** @override */
  getData() {
    const data = super.getData();
    return data;
  }

  /* -------------------------------------------- */
```

<!--- {% endraw %} --->

## setPosition()

This is a small override to handle remembering the sheet's position.

<!--- {% raw %} --->

```js
  /** @override */
  setPosition(options = {}) {
    const position = super.setPosition(options);
    const sheetBody = this.element.find(".sheet-body");
    const bodyHeight = position.height - 192;
    sheetBody.css("height", bodyHeight);
    return position;
  }

  /* -------------------------------------------- */
```

<!--- {% endraw %} --->

## activateListeners()

As with the actor sheet, this is where you would activate listeners and events for your item sheet. For example, if you had logic that happened on click or edit, or if you had a roll button within the item sheet, that could go in here. <!-- {% raw %} -->`html`<!-- {% endraw %} --> is a jQuery object that you can use to find other elements, like <!-- {% raw %} -->`html.find('.rollable')`

<!--- {% raw %} --->

```js
  /** @override */
  activateListeners(html) {
    super.activateListeners(html);

    // Everything below here is only needed if the sheet is editable
    if (!this.options.editable) return;

    // Roll handlers, click handlers, etc. would go here.
  }
```

<!--- {% endraw %} --->

## Wrapping up

Don't forget closing brackets!

<!--- {% raw %} --->

```js
}
```

<!--- {% endraw %} --->

---

* **Prev:** [Extending the Item class](https://foundry-vtt-community.github.io/wiki/SD09-Extending-the-Item-class)
* **Next:** [Creating rollable buttons with event listeners](https://foundry-vtt-community.github.io/wiki/SD11.1-Creating-rollable-buttons-with-event-listeners)