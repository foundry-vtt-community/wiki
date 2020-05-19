Before we start diving into development, there are a few useful things to know as background information.

## HTML, CSS, and JS

Systems are built using HTML, CSS, and Javascript. Teaching those is outside the scope of this tutorial, but there are many great courses out there on different platforms such as:

* [https://www.freecodecamp.org/learn](https://www.freecodecamp.org/learn)
* [https://www.codecademy.com/](https://www.codecademy.com/)
* [https://www.udemy.com/courses/development/web-development/](https://www.udemy.com/courses/development/web-development/)
* [https://www.khanacademy.org/](https://www.khanacademy.org/)

## Should I use scripts or ES modules?

In your system.json file, there will be sections for both <!-- {% raw %} -->`scripts`<!-- {% endraw %} --> and <!-- {% raw %} -->`esmodules`<!-- {% endraw %} -->. This tutorial (and most systems developed currently) use the latter option, but it's also a bit more advanced. If you're struggling with them, it may be easier to just put all of your system code in a few <!-- {% raw %} -->`<!-- {% endraw %} -->.js`<!-- {% endraw %} --> files that you include in the scripts section of your system.json

To use ES modules, you'll want to load a single <!-- {% raw %} -->`mysystemname.js`<!-- {% endraw %} --> file in your <!-- {% raw %} -->`esmodules`<!-- {% endraw %} --> section of system.json. That file will typically have an import section at the top that imports classes from other Javascript files that you create, and your hooks for Foundry will also be placed in there. We'll do a deeper dive on how that works later in the tutorial.

To use scripts,  you'll load one or more Javascript files, such as <!-- {% raw %} -->`mysystemname.js`<!-- {% endraw %} --> in your <!-- {% raw %} -->`scripts`<!-- {% endraw %} --> section of system.json. That file will include all of your classes, hooks, and any code necessary to run your system. It's harder to organize because of that, but you also don't have to worry about exporting or importing your classes.

## CSS preprocessors

The more CSS you add to your system, the more difficult it will be to maintain over time. One of the most powerful tools to help keep it organized is to use a CSS preprocessor like [Less](http://lesscss.org/) or [SCSS/Sass](https://sass-lang.com/). Using a preprocessor will allow you to break up your CSS files into partials that can later be combined into a single file, nest your styles for more readable code, and use variables for things like colors, padding, and fonts.

The Boilerplate System we're using in this tutorial includes support for SCSS, but you can also just work directly with the CSS files instead if you prefer. For a great implementation that uses Less, download the dnd5e system.

To build the SCSS files in this system, you'll need to go into the system's directory in your terminal, run <!-- {% raw %} -->`npm install`, and then <!-- {% raw %} -->`npm run gulp`<!-- {% endraw %} --> whenever you want to compile the SCSS into CSS. Using the gulp command will also kick off a watch process that will watch for additional changes.

## Handlebars

FoundryVTT uses [Handlebars](https://handlebarsjs.com/guide/#what-is-handlebars) to interpret its HTML templates and add basic support for things like variables, if statements, and loops. Handlebars is not a programming language like Javascript is, so if you want to do something more advanced than outputting a variable or iterating over a loop, you'll probably need to either handle the code for that in your actor/item's data methods in JS, or you can create a new Handlebars helper to add additional logic to your Handlebars files. For example, the Boilerplate System includes a Handlebars helper called <!-- {% raw %} -->`concat`<!-- {% endraw %} --> that will combine variable strings such as <!-- {% raw %} -->`{{concat "string 1, " "string 2"}}`

## What about 3rd party libraries?

Sometimes you need to include 3rd party libraries to do additional things, such as if you wanted to use [Tagify](https://github.com/yairEO/tagify) to make a tagging widget. Using those libraries is beyond the scope of this tutorial, but whenever I need to install additional libraries, I make a <!-- {% raw %} -->`lib`<!-- {% endraw %} --> directory inside my system to place their files, and then include them in the <!-- {% raw %} -->`scripts`<!-- {% endraw %} --> and <!-- {% raw %} -->`styles`<!-- {% endraw %} --> section of system.json

## Localization (i18n)

**Localization is extremely important if you're making a publicly available system!**

It's always more effort to go back and localize a system after it's developed, so if you're making a publicly available system, I strongly recommend localizing it from the start. I'll go into more detail on this as we begin developing our system, but to localize your system you'll need to make an <!-- {% raw %} -->`en.json`<!-- {% endraw %} --> file (or whatever your default language is) in your system's <!-- {% raw %} -->`lang`<!-- {% endraw %} --> dir, and add that to your system.json file. <!-- {% raw %} -->`en.json`<!-- {% endraw %} --> consists of key/value pairs where you can specify what the text should be for the keys, and then in your templates you would do <!-- {% raw %} -->`{{localize "KEY.name" }}`<!-- {% endraw %} --> to output its localized version.

---

* **Prev:** [Getting an empty system together](https://foundry-vtt-community.github.io/wiki/SD01-Getting-started)
* **Next:** [system.json](https://foundry-vtt-community.github.io/wiki/SD03-system.json)