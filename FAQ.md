<!--tl=2-->
<!--ts-->
   * [Frequently Asked Questions](#frequently-asked-questions)
      * [How Do I Access Foundry VTT?](#how-do-i-access-foundry-vtt)
      * [How Do I Link My Patreon to Discord?](#how-do-i-link-my-patreon-to-discord)
      * [How do I enable WebGL?](#how-do-i-enable-webgl)
      * [How Do I Connect to an IPv6 Address?](#how-do-i-connect-to-an-ipv6-address)
      * [How Do I Install Modules?](#how-do-i-install-modules)
      * [I Forgot My Player Access Keys!](#i-forgot-my-player-access-keys)
      * [Where Can I Place Content In Foundry?](#where-can-i-place-content-in-foundry)
      * [How Do I Apply Damage?](#how-do-i-apply-damage)
      * [How Do I Create a Custom Character Sheet](#how-do-i-create-a-custom-character-sheet)
      * [How Do I Improve Performance?](#how-do-i-improve-performance)
      * [How Do Walls Affect Performance?](#how-do-walls-affect-performance)
   * [Suggestions/Ideas/Issues](#suggestionsideasissues)
      * [I Have a Suggestion/Idea/Issue](#i-have-a-suggestionideaissue)
<!--te-->

# Frequently Asked Questions

## How Do I Access Foundry VTT?
Access to FVTT Beta is through Patreon. On release it will be a one-time purchase. Release is tentatively slated for Q2-2020. Price is not yet set. Only the host will need a license, everyone else can login via a webbrowser.

## How Do I Link My Patreon to Discord?
Refer to Patreon's instructions [here](https://support.patreon.com/hc/en-us/articles/212052266-How-do-I-receive-my-Discord-role-#h_21f22930-84c5-4950-b6b1-3e83312f66dc).

## How do I enable WebGL?

**Chrome** - `chrome://settings` -> "System" -> Toggle "Use hardware acceleration when available" to on

**Firefox** - `about:preferences` -> Performance -> Uncheck "Use recommended performance settings" -> Check "Use hardware acceleration when available"

## How Do I Connect to an IPv6 Address?
Open your browser of choice and enter the address like this: `http://[IP:v6:AD:RE:SS]:PORTNUMBER`

- Paste the full IPv6 Address between the `[` `]`
- Port number by default is 3000

## How Do I Install Modules?
Check out the [Modules](https://foundry-vtt-community.github.io/wiki/Modules/) page for instructions.

## I Forgot My Player Access Keys!
Check `/worlds/<worldname>/data/users.db`.

## Where Can I Place Content In Foundry?
You can place anything you want in the `public` folder located at `resources/app/public`.

## How Do I Apply Damage?
There is an option to apply damage from a roll. Right click on the damage and a context menu will show up that will apply that damage or healing to the select token.

## How Do I Create a Custom Character Sheet
Start by downloading the example `HTML` and `JS` files provided by Atropos:

1. [my-actor-sheet.js](https://cdn.discordapp.com/attachments/554492873190670336/616309044604436511/my-actor-sheet.js) - This is the JavaScript that defines the sheet and registers it with the Foundry VTT system 
2. [my-actor-sheet.html](https://cdn.discordapp.com/attachments/554492873190670336/616309067513593856/my-actor-sheet.html) - This is the HTML template where you define the structure and templating for your sheet

**NOTE** - This does require knowledge of `CSS` for styling.

## How Do I Improve Performance?
One easy way to improve performance is by disabling soft shadows. You can do this in game by clicking **Game Settings** -> **Configure Settings** and uncheck **Enable Soft Shadows**.

You can also check what is affecting performance by opening the developer console (`F12`) and running the following commands:
- **Number of Walls**: `console.log(canvas.walls.placeables.length);`
- **Number of Light Sources**: `console.log(canvas.lighting.placeables.length);`
- **Number of Tokens**: `console.log(canvas.tokens.placeables.length);`
- **Scene Dimensions**: `console.log(canvas.dimensions);`

Evaluate the results against the hardware of your machine on the client side

## How Do Walls Affect Performance?
What matter for wall performance the the amount of *unique* wall endpoints, rather than the amount of walls themselves. In short longer walls are better than shorter walls.

- **Terrain Walls** have the same performance as a **Regular Wall**.
- **One-Way Walls** are more computationally intensive, as it has to check the orientation of the ray collision.

# Suggestions/Ideas/Issues

## I Have a Suggestion/Idea/Issue
Check the official [issue tracker](https://gitlab.com/foundrynet/foundryvtt/issues) first, and if it's not listed, jump on [Discord](https://discordapp.com/invite/DDBZUDf) and hit up the #vtt-suggestions or #vtt-testing channels (don't forget to search for your suggestion/idea/issue first before posting again!)