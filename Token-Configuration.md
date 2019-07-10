First, an important distinction. There are two different kinds of token configuration windows. The first, opened directly from an actor sheet on the sidebar is the **default token configuration**, that is to say, how new tokens dragged on the scene will be initially created. Once on the scene, a specific token’s configuration can be **changed from the default**. The window to do so can either be opened by double right-clicking the token itself, or clicking the cogwheel in the token HUD.

In the token configuration screen, multiple tabs at the top let you access different settings for the token, whichever template you are editing (default or specific). The Update Token button is essentially a “save settings” button, which updates the token’s settings. The Assign Token button, only visible in the default token window, let’s you set a selected token’s specific token configuration become the default.

# Character Tab
## Nameplate Settings
The first field in the character tab is the Nameplate field, which lets you edit the name of the token. It can differ from it’s actor name, and can be shown or not with various behaviours in the Show Nameplate drop down menu. The actor the token represents can also be changed in the Represented Actor field (no clue what use case to use as example here, if anyone has an idea).

## Link Actor Data
This option should only be selected for unique actors, such as PCs and important unique NPCs. They tie the token data to the actor sheet. By default, a ressources tracked on the token is tracked independently from the parent actor, since the same actor could spawn multiple tokens, such as a horde of goblins which all have the same “stat block” but will take different amounts of damage in a combat.

## Token Disposition
This section has three settings to visually represent the token’s feelings towards the PCs with a colored border around the token: green for friendly, yellow for neutral, and red for hostile.

# Image Tab
The image tab is where you can define how the token appears on the canvas.

## Image Path
The Token Image Path field is the most important field in this section: it is this field which defines the source image for a token. This path can be an URL or a file path relative to the public folder in the hosting install of FVTT. This path can be typed in, but you should usually just be able to use the file explorer by clicking the button beside the text field.

## File Explorer

## Wildcards

## Token Size
The width and height values specified here are set to a number of grid squares (or hexes) and determine how much space the token takes on the field.
The scale slider only changes the image scale without changing the actual space taken by the token unit. A number higher than 1 results in a bigger image while a number below 1 makes it appear smaller.