In addition to the JS classes that define them, actors and items also have HTML templates that define the structure of your character and item sheets. In the Boilerplate System, these are placed in `/templates/actor/actor-sheet.html` and `/templates/item/item-sheet.html`. These paths are not discovered automatically; you have to define specify their full path in your ActorSheet and ItemSheet class' defaultOptions() method. You'll probably add many more templates than just these two as your system gets further into development, but the process is the same for all of them.

HTML templates in Foundry use [Handlebars](https://handlebarsjs.com/guide/) for their templating engine. If you're using a code editor like [Visual Studio Code](https://code.visualstudio.com/), you can set the syntax highlighting mode to Handlebars and get useful color coding to help recognize the various statements and variables in your templates.

Let's start by taking a look at how the `actor-sheet.html` template is laid out at a high level.

<!--- {% raw %} --->

```handlebars
<form class="{{cssClass}} flexcol" autocomplete="off">

    {{!-- Sheet Header --}}
    <header class="sheet-header">
        {{!-- Header stuff goes here --}}
        <img class="profile-img" src="{{actor.img}}" data-edit="img" title="{{actor.name}}" height="100" width="100"/>
        <div class="header-fields">
            <h1 class="charname"><input name="name" type="text" value="{{actor.name}}" placeholder="Name"/></h1>
            <div class="resources grid grid-2col">{{!-- resources here --}}</div>
            <div class="abilities grid grid-3col">{{!-- abilities here --}}</div>
        </div>
    </header>

    {{!-- Sheet Tab Navigation --}}
    <nav class="sheet-tabs tabs" data-group="primary">
        <a class="item" data-tab="description">Description</a>
        <a class="item" data-tab="items">Items</a>
    </nav>

    {{!-- Sheet Body --}}
    <section class="sheet-body">
		{{!-- Tab content goes here --}}
    </section>
</form>
```

<!--- {% endraw %} --->

And here's an annotated version of what that looks like:

![boilerplate character sheet annotated](https://mattsmithin.nyc3.digitaloceanspaces.com/assets/boilerplate-character.png)

## The `<form>`

The element that surrounds our entire sheet is a `<form>` element with a variable that's outputting `{{cssClass}}`. This is a combined version of the array of CSS classes we made earlier in the actor-sheet.js file's defaultOptions() method. You can also include classes and other attributes directly in the template, as we did here with `flexcol`. The flexcol class is a helper class provided by Foundry that can be used to layout things vertically without having to write additional CSS. There are several of those included by Foundry, and the Boilerplate System also includes several for grids.

> ### Basic sheet layout in Boilerplate System
>
> This system includes a handful of helper CSS classes to help you lay out your sheets if you're not comfortable diving into CSS fully. Those are:
>
> -   `flexcol`: Included by Foundry itself, this lays out the child elements of whatever element you place this on vertically.
> -   `flexrow`: Included by Foundry itself, this lays out the child elements of whatever element you place this on horizontally.
> -   `flex-center`: When used on something that's using flexrow or flexcol, this will center the items and text.
> -   `flex-between`: When used on something that's using flexrow or flexcol, this will attempt to place space between the items. Similar to "justify" in word processors.
> -   `flex-group-center`: Add a border, padding, and center all items.
> -   `flex-group-left`: Add a border, padding, and left align all items.
> -   `flex-group-right`: Add a border, padding, and right align all items.
> -   `grid`: When combined with the `grid-Ncol` classes, this will lay out child elements in a grid.
> -   `grid-Ncol`: Replace `N` with any number from 1-12, such as `grid-3col`. When combined with `grid`, this will layout child elements in a grid with a number of columns equal to the number specified.

## The `<header>`

The header element is used to create the header section of the form where we put a small amount of important information about our character that should always be visible, like their name, hit points, and ability scores. This will vary heavily depending on your system's needs. Let's step through each section of the header:

<!--- {% raw %} --->

```handlebars
    {{!-- Sheet Header --}}
    <header class="sheet-header">
        <img class="profile-img" src="{{actor.img}}" data-edit="img" title="{{actor.name}}" height="100" width="100"/>
        <div class="header-fields">
            <h1 class="charname"><input name="name" type="text" value="{{actor.name}}" placeholder="Name"/></h1>
            {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

The first element in our header is the actor's image. Aside from adding additional classes or tweaking the height/weight values, your actor images should always follow this pattern if they need to be editable by foundry. We're printing out the path to the image with the `{{actor.img}}` variable, and the `data-edit="img"` tells Foundry that this is an image that should be editable on click.

> ### Variables in Handlebars
> If you're inside an actor-sheet template, the `actor` object will be available for printing things such as the actor name and actor image source with variables such as `actor.name` and `actor.img`. The `actor.data.data` object is also available at a more convenient `data` variable, so for properties that are unique to your system you can print values such as `{{data.health.value}}`.

### The resources grid

The next item in our `<div class="header-fields">` div is the resources grid.

<!--- {% raw %} --->

```handlebars
            {{!-- ...continued... --}}
            <div class="resources grid grid-2col">
              <div class="resource flex-group-center">
                  <label for="data.health.value" class="resource-label">Health</label>
                  <div class="resource-content flexrow flex-center flex-between">
                    <input type="text" name="data.health.value" value="{{data.health.value}}" data-dtype="Number"/>
                    <span> / </span>
                    <input type="text" name="data.health.max" value="{{data.health.max}}" data-dtype="Number"/>
                  </div>
              </div>
              <div class="resource flex-group-center">
                  <label for="data.power.value" class="resource-label">Power</label>
                  <div class="resource-content flexrow flex-center flex-between">
                    <input type="text" name="data.power.value" value="{{data.power.value}}" data-dtype="Number"/>
                    <span> / </span>
                    <input type="text" name="data.power.max" value="{{data.power.max}}" data-dtype="Number"/>
                  </div>
              </div>
          </div>
          {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

In this case, we have a container div with the classes `resources`, `grid`, and `grid-2col`. The later two classes are the ones driving the layout here; any elements immediately inside the resources div (or `resource` divs in this case) will be laid out as a two column grid. We're also using the `flex-group-center` class on the individual `resource` divs to add some padding, a border, and text centering on them.

Each resource has a few fields. There's a label with a special `resource-label` class that makes it bold and uppercase. We also have a `resource-content` div with several different flex classes on it to lay out its contents in a row.

Finally, we have our inputs. Text inputs in Foundry always follow this pattern:

<!--- {% raw %} --->

```handlebars
<input type="text" name="data.health.value" value="{{data.health.value}}" data-dtype="Number" />
```

<!--- {% endraw %} --->

Here's what that's doing:

- **name**: This attribute is used to tell Foundry what field on the actor should be updated when changes are made. This should be plain text, so _don't_ put it inside `{{ variable }}` brackets.
- **value**: This is the current value of the input, and the one the user can change. Because this is the value, we need to put it in `{{ variable }}` brackets so that Foundry outputs the correct value for it.
- **data-dtype**: This is a special attribute that Foundry uses to validate the form input. There are several, but the most common ones are `Number` for numbers, `String` for text, and `Boolean` for true/false checkboxes.

### The abilities `<div>`

The abilities div is very similar to resources, but in this case we have a group of related abilities that can be looped over.

<!--- {% raw %} --->

```handlebars
          {{!-- ...continued... --}}
          <div class="abilities grid grid-3col">
            {{#each data.abilities as |ability key|}}
              <div class="ability flexrow flex-group-center">
                <label for="data.abilities.{{key}}.value" class="resource-label">{{key}}</label>
                <input type="text" name="data.abilities.{{key}}.value" value="{{ability.value}}" data-dtype="Number"/>
                <span class="ability-mod">{{numberFormat ability.mod decimals=0 sign=true}}</span>
              </div>
            {{/each}}
          </div>
        </div>
    </header>
    {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

First, we're using the same `grid` classes as before, except now we're doing `grid-3col` for a three column layout.

The big difference is that we're running a loop with `{{#each}}`. Let's look at that statement in more detail:

<!--- {% raw %} --->

```handlebars
{{#each data.abilities as |ability key|}}
  {{!-- stuff --}}
{{/each}}
```

<!--- {% endraw %} --->

An each block starts with `#each` and ends with `/each`. The first thing after the opening `{{#each` is the object or array we want to iterate over, or in this case `data.abilities`.

You can either iterate over just the values, which would be `data.abilities as ability` or over the values with the keys available as well, which is what we're doing with `data.abilities as |ability key|`. By doing that we can access the index/key using the `{{key}}` variable, which would evaluate to something like "str", "dex" or "con". The `{{ability}}` variable will give us the object for each ability, which will allow us to print out the current value with `{{ability.value}}`.

Here's what the actual ability input looks like:

<!--- {% raw %} --->

```handlebars
<input type="text" name="data.abilities.{{key}}.value" value="{{ability.value}}" data-dtype="Number"/>
```

<!--- {% endraw %} --->

The first thing to notice is that **name** and **value** are much different than they were in our earlier example! The name attribute needs to be the exact the set of properties that Foundry would use to update the value, so we're mostly printing it out as plain text except for the part that would be "str" or "dex". For that we have to print out the current `{{key}}`. So in our loop we're using `data.abilities.{{key}}.value` for the name, which will get rendered as something like `data.abilities.str.value`.

The value is a bit different though. Because we already have the current ability object in the `{{ability}}` variable, we can just print out `{{ability.value}}` without worrying about the full `data.abilities` structure.

Finally, let's take a look at the ability modifier:

<!--- {% raw %} --->

```handlebars
<span class="ability-mod">{{numberFormat ability.mod decimals=0 sign=true}}</span>
```

<!--- {% endraw %} --->

The user doesn't need to edit this, so we're just outputting the value as content inside a span element rather than the value on an input. Why is it a span? If you just need an element that doesn't have semantic meaning the way a `<p>` tag does for paragraphs, the `<div>` and `<span>` tags are good catchalls for grouping content. Div will typically stretch out and take up a whole row horizontally (unless you change that with CSS) while spans are inline and will only take up as much space as their text requires.

Something we're doing different for the modifier is that we're using the `numberFormat` Handlebars helper. This is a special helper that Foundry includes and it allows you to format numbers with `+` and `-` signs depending on their value, along with rounding decimals. In this case we're using numberFormat on `ability.mod`, which we derived earlier, and setting the decimals and `+/-` sign to true.

## The `<nav>` tabs

The navigation (nav) element is used to create our sheet's tabs for navigation to multiple pages.

<!--- {% raw %} --->

```handlebars
    {{!-- ...continued... --}}
    {{!-- Sheet Tab Navigation --}}
    <nav class="sheet-tabs tabs" data-group="primary">
        <a class="item" data-tab="description">Description</a>
        <a class="item" data-tab="items">Items</a>
    </nav>
    {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

Tabs are created as a `<nav>` element with a `tabs` class and a `data-group`. The exact data-group name doesn't really matter, as long as it also matches up tab content divs we'll make later. For instance, you could make `data-group="primary"` for one set of tabs and `data-group="secondary"` for a completely unrelated set of tabs (or even nested tabs).

Each tab inside the name if an `<a>` link with a `data-tab` attribute. Much like `data-group`, the contents of `data-tab` don't matter as long as they exactly match a `data-tab` attribute on your tab content div that gets created later.

## The `<section>` body

Finally, we also have a `<section>` element that's used to create the body of sheet where the various pages (which are navigated to via tabs) will live. This doesn't have to be a section element; it could have also been something else like a `<div>`, but sections can be used to tell the browser "this is a discreet chunk of related content", such as multiple paragraphs in a book that are all under the same headline.

Because we're using tabs on this sheet, each item inside sheet-body is a tab that also needs `data-group` and `data-tab` attributes. Here's the markup for that in the Boilerplate System:

<!--- {% raw %} --->

```handlebars
    {{!-- ...continued... --}}
    {{!-- Sheet Body --}}
    <section class="sheet-body">

        {{!-- Biography Tab --}}
        <div class="tab biography" data-group="primary" data-tab="description">
            {{editor content=data.biography target="data.biography" button=true owner=owner editable=editable}}
        </div>

        {{!-- Owned Items Tab --}}
        <div class="tab items" data-group="primary" data-tab="items">
            <ol class="items-list">
                <li class="item flexrow item-header">
                  <div class="item-image"></div>
                  <div class="item-name">Name</div>
                  <div class="item-controls">
                    <a class="item-control item-create" title="Create item" data-type="item"><i class="fas fa-plus"></i> Add item</a>
                  </div>
                </li>
            {{#each actor.items as |item id|}}
                <li class="item flexrow" data-item-id="{{item._id}}">
                    <div class="item-image"><img src="{{item.img}}" title="{{item.name}}" width="24" height="24"/></div>
                    <h4 class="item-name">{{item.name}}</h4>
                    <div class="item-controls">
                        <a class="item-control item-edit" title="Edit Item"><i class="fas fa-edit"></i></a>
                        <a class="item-control item-delete" title="Delete Item"><i class="fas fa-trash"></i></a>
                    </div>
                </li>
            {{/each}}
            </ol>
        </div>

    </section>
    {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

### The biography tab

The biography tab in the Boilerplate System is both an example of how to make a tab and how to use a TinyMCE editor.

<!--- {% raw %} --->

```handlebars
{{!-- Biography Tab --}}
<div class="tab biography" data-group="primary" data-tab="description">
  {{editor content=data.biography target="data.biography" button=true owner=owner editable=editable}}
</div>
```

<!--- {% endraw %} --->

First, we have the `tab` class to establish that this is a tab, and a `biography` class that we could use for more specific CSS styling if needed. The `data-group` attribute lets us associate with the primary tabs group, and the `data-tab` attribute tells Foundry that this is specifically the description tab (which we defined earlier in the `<nav>` element).

`{{editor}}` is a special Handlebars helper that will return a TinyMCE text editor. You'll usually want to format it very similar to this example, substituting the `content` and `target` properties with whatever data property you want the editor to make changes to.

### The owned items tab

The owned items tab starts out much like the biography tab:

<!--- {% raw %} --->

```handlebars
<div class="tab items" data-group="primary" data-tab="items">
{{!-- ...continued... --}}
```

<!--- {% endraw %} --->

The contents are significantly different though. For owned items, we're displaying it in a table-like format using ordered lists.

<!--- {% raw %} --->

```handlebars
  {{!-- ...continued... --}}
  <ol class="items-list">
    <li class="item flexrow item-header">
      <div class="item-image"></div>
      <div class="item-name">Name</div>
      <div class="item-controls">
        <a class="item-control item-create" title="Create item" data-type="item"><i class="fas fa-plus"></i> Add item</a>
      </div>
    </li>
    {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

First, we're defining an ordered listed with the `items-list` class. We need a header though, so we manually create an `<li>` tag with the `item`, `flexrow`, and `item-header` classes. The `item-header` class is used to let the CSS included with Boilerplate know that this is a header for a list and should use bold font weights.

We then have one div for each column of our items, the image, name, and controls. We don't need a label for the image, so it's left empty, but we do still need the empty div so that the flexbox layout matches our item rows later. Item name has the name label included in it. For item controls, we've actually added an `<a>` tag that's used to create new items rather than just putting a label that says "controls." We'll come back to this in a later step of the tutorial, but the `item-create` class will be used for a click event listener, and the `data-type` attribute will be used to specify the item type to create (such as item, spell, or feat). You can also go back in the tutorial to the `actor-sheet.js` and in the `activateListeners()` method, you'll see where click listeners were added for this functionality.

Up next, we have the loop to print out all of the owned items:

<!--- {% raw %} --->

```handlebars
    {{!-- ...continued... --}}
    {{#each actor.items as |item id|}}
      <li class="item flexrow" data-item-id="{{item._id}}">
        <div class="item-image"><img src="{{item.img}}" title="{{item.name}}" width="24" height="24"/></div>
        <h4 class="item-name">{{item.name}}</h4>
        <div class="item-controls">
          <a class="item-control item-edit" title="Edit Item"><i class="fas fa-edit"></i></a>
          <a class="item-control item-delete" title="Delete Item"><i class="fas fa-trash"></i></a>
        </div>
      </li>
    {{/each}}
    {{!-- ...continued... --}}
```

<!--- {% endraw %} --->

As we did earlier with abilities, we can iterate over an actor's items. This is a bit of a simple loop as we're iterating over _all_ of an actor's items, whether those are items, spells, feats, or any other sub-type that we've defined. We'll rework this in a later step of the tutorial to break it up into sorted groups of the different item types, but for now this will allow us to iterate over everything.

For the most part, the `<li>` tags in this `#each` loop are very similar to the ones we made for the header row, but there are a few differences. First, we have a special `data-item-id="{{item._id}}"` attribute on the list item. Having this is very important to making your life easier, because by having it on the parent list item, any links that we make on one of the elements nested in the list item will be able to grab that ID for usage in our Javascript.

Next, we're outputting the `item.img` and `item.name` variables as needed.

And finally, we're outputting the item controls. Notice that the controls have `item-edit` and `item-delete` classes, similar to the `item-create` class we added to the item-head div earlier? Those are two additional classes that have click listeners defined in `actor-sheet.js`. Let's step back to `actor-sheet.js` and take a look at the `activateListeners()` method:

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

What's happening here? First, we're activating any listeners that Foundry itself defines with `super.activateListeners(html)`.

Second, we're returning early if the sheet isn't editable (which usually means an observer has it open rather than the sheet owner).

Third, we're defining a click listener for `item-create`. We went into detail earlier about what the `_onItemCreate()` method did, so we'll skip over that here.

Fourth, we're defining click listeners for `item-edit` and `item-delete`. These two listeners are similar; both of them grab the element for the list item that's a parent of the button being clicked, which is what `$(ev.currentTarget).parents('.item')` does. Since we have the `data-item-id` attribute on the list items, we can than use the actor's methods to either get the owned item and render it's item sheet or delete the owned item, depending on which listener we're in. If we're deleting the item, we also do a small animation with `li.slideUp()` to animate getting rid of the item.

## Wrapping up

Jumping back over to the actor-sheet.html template, we've covered the list of the logic in it for the Boilerplate system. Don't forget your closing tags though!

<!--- {% raw %} --->

```handlebars
            {{!-- ...continued... --}}
            </ol>
        </div>
    </section>
</form>
```

<!--- {% endraw %} --->

---

- **Prev:** [Extending the ActorSheet class](https://foundry-vtt-community.github.io/wiki/SD07-Extending-ActorSheet-class)
- **Next:** [Extending the Item class](https://foundry-vtt-community.github.io/wiki/SD09-Extending-the-Item-class)