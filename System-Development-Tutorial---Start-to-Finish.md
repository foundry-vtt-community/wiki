Welcome to my system development tutorial for FoundryVTT! My goal is to guide you through system development with little to no knowledge of Foundry or the languages it uses. At first we'll walk through the steps to create relatively simple systems that allow you to collect data for things like stats and attributes and calculate modifiers for them, but eventually we'll get into more advanced topics like making dice rolls from your sheet or letting items be converted into macros.

If you have any questions, you can find me on the Foundry discord as @asacolips#1867. And with that, let's move onto to the tutorial!

- [Getting an empty system together](https://foundry-vtt-community.github.io/wiki/SD01-Getting-started)
	- Start with a boilerplate system
	- Using SWS
	- Using a CLI
- [Stuff to be aware of](https://foundry-vtt-community.github.io/wiki/SD02-Stuff-to-be-aware-of)
	- Scripts or ES6 modules?
	- CSS preprocessors
	- Handlebars
	- What about 3rd party libraries?
	- Localization
- [system.json](https://foundry-vtt-community.github.io/wiki/SD03-system.json)
- [template.json](https://foundry-vtt-community.github.io/wiki/SD04-template.json)
	- Defining actor and item types
- [Creating your main system javascript file](https://foundry-vtt-community.github.io/wiki/SD05-Creating-your-main-JS-file)
- [Extending the Actor class](https://foundry-vtt-community.github.io/wiki/SD06-Extending-the-Actor-class)
	- Basic data vs. derived data
	- Creating derived values with prepareData()
	- _prepareCharacterData()
- [Extending the ActorSheet class](https://foundry-vtt-community.github.io/wiki/SD07-Extending-ActorSheet-class)
	- defaultOptions
	- getData()
	- activateListeners()
- [Creating HTML templates for your actor sheets](https://foundry-vtt-community.github.io/wiki/SD08-Creating-HTML-templates-for-your-actor-sheets)
- [Extending the Item class](https://foundry-vtt-community.github.io/wiki/SD09-Extending-the-Item-class)
- [Extending the ItemSheet class](https://foundry-vtt-community.github.io/wiki/SD10-Extending-the-ItemSheet-class)
- Other things to do on actor sheets
	- [Creating rollable buttons with event listeners](https://foundry-vtt-community.github.io/wiki/SD11.1-Creating-rollable-buttons-with-event-listeners)
	- [Grouping items by type](https://foundry-vtt-community.github.io/wiki/SD11.3-Grouping-items-by-type)
	- [Separating item types into tabs](https://foundry-vtt-community.github.io/wiki/SD11.4-Separating-item-types-into-tabs)
	- [Adding macrobar support for your items](https://foundry-vtt-community.github.io/wiki/SD16-Adding-macrobar-support-to-your-Items)

## Sections that are Work-in-Progress

In addition to the above, there are several more sections that will be added to this tutorial over time! Check back in every few weeks to see if any additions have been made. If there's a topic related to system development that you would like to see added to this list, shoot me a message on Discord!

- Other things to do on actor sheets
	- Creating rollable buttons with dialogs
	- Creating item-like data structures
	- Querying for entities with map and filter
	- When in doubt, look at other systems
- CONFIG and things to do with it
- More Localization
- TabsV2
- Flags
- System Settings
- Making things draggable in your sheet
- Overriding core behaviors (like the combat tracker)
- Development patterns to be aware of in the API

<!--- {% raw %} --->
```handlebars
    {{!-- ...continued... --}}
    {{!-- Sheet Tab Navigation --}}
    <nav class="sheet-tabs tabs" data-group="primary">
        <a class="item" data-tab="description">Description</a>
        <a class="item" data-tab="items">Items</a>
        <a class="item" data-tab="features">Features</a>
        <a class="item" data-tab="spells">Spells</a>
    </nav>
    {{!-- ...continued... --}}
```
<!--- {% endraw %} --->