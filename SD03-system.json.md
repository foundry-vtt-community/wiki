Once you've created your system, you'll need to make some changes to system.json. Here's what it looks like for the Boilerplate System by default:

<!--- {% raw %} --->

```json
{
  "name": "boilerplate",
  "title": "Boilerplate",
  "description": "The Boilerplate system for FoundryVTT!",
  "version": "1.0.0",
  "minimumCoreVersion": "0.5.5",
  "compatibleCoreVersion": "0.5.5",
  "templateVersion": 2,
  "author": "Asacolips",
  "esmodules": ["module/boilerplate.js"],
  "styles": ["css/boilerplate.css"],
  "scripts": [],
  "packs": [],
  "languages": [
    {
      "lang": "en",
      "name": "English",
      "path": "lang/en.json"
    }
  ],
  "gridDistance": 5,
  "gridUnits": "ft",
  "primaryTokenAttribute": "health",
  "secondaryTokenAttribute": "power",
  "url": "",
  "manifest": "",
  "download": "",
  "license": "LICENSE.txt"
}
```

<!--- {% endraw %} --->

For a full breakdown of each of those properties head to [https://foundryvtt.com/article/system-development/](https://foundryvtt.com/article/system-development/). But there a few important ones to take a look at in detail:

- **name**: Your system's machine-safe name, such as `mysystemname` or `dnd5e`.
- **minimumCoreVersion**: The minimum core version of Foundry required to install this system. If there are API changes in Foundry itself that you have to make significant updates for, you'll want to update this number.
- **compatibleCoreVersion**: The most recently tested version of Foundry for this system. If Foundry is newer than the version listed here, users will receive a warning when trying to install or use your system. You'll need to update this frequently.
- **templateVersion**: Set this value to 2. Previously, Foundry supported a different template.json syntax that has since been removed, so this will tell Foundry that your system is using the current template syntax, version 2.
- **esmodules**: An array of Javascript files to import as ES modules. If you need to add multiple files, you can do a comma separated list inside the `[]` brackets.
- **styles**: An array of CSS files to use for your system's styling.
- **scripts**: An array of Javascript files to include in your system. These files will not use the export/import syntax that ES modules use.
- **packs**: Compendium packs. Each pack will be an object where you specify the name, system, path, and entity type. The `dnd5e` system has several great examples of creating a compendium, and more info can be found at [https://foundryvtt.com/article/compendium/](https://foundryvtt.com/article/compendium/).
- **languages**: Any language definitions that you create will need to be listed here. Boilerplate System comes with an included `en.json` language file.
- **url**: The link to your system's homepage, such as the Github or Gitlab page for it.
- **manifest**: The raw link to this `system.json` file. Foundry uses this to find out information about your system for update and install purposes.
- **download**: The raw link to download a zip file of your system. This can be built via custom build tools, but Github and Gitlab both generate zip files from your master branch that you can use here.

- **Prev:** [Stuff to be aware of](https://foundry-vtt-community.github.io/wiki/SD02-stuff-to-be-aware-of)
- **Next:** [template.json](https://foundry-vtt-community.github.io/wiki/SD04-template.json)