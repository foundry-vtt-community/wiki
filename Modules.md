Modules enhance or replace functionality within Foundry VTT. Most modules consist of a `module.json` file that describes the module and contains some metadata about it, and a `<module name>.js` file that contains the module code. Some modules also include `css` and `html` files.

# Finding Modules
Community created modules can be found via the [Community Modules](https://foundry-vtt-community.github.io/wiki/Community-Modules/) wiki page, or in the [Community Modules Repo](https://github.com/foundry-vtt-community/modules)

# Installing Modules

## Via Manifest URL
1. Open the Foundry setup page in a web browser
2. Click on the Add-on Modules tab
3. Click the Install Module button
4. Paste the Manifest URL to the Module being installed
5. Click Install 

## Manually
1. Placing the module files under `\resources\app\public\modules\<module name>` inside your Foundry VTT installation folder. 
2. Restart the Foundry VTT server
3. Log back into Foundry VTT as the GameMaster
4. Click the Help button
5. Click Manage Modules under the game system heading (eg. D&D 5th Edition)
6. Find the newly installed module and place a checkmark next to the name, then click Update Modules at the bottom of the list to activate it


# Developing Modules
Modules are developed using the Foundry VTT API which is documented on the official [Foundry VTT site](http://foundryvtt.com/pages/api.html).

