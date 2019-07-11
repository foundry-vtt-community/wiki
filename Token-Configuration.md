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
The file explorer let's you select files in the public folder to automatically input the image path. The upward arrow at the top of the window let's you navigate out of the current folder to its parent, but does not let you get further than `/public`, while the field beside it indicates where you currently are in `/public`. This is also where any file uploaded using the _Choose file_ to upload at the bottom will end up when uploaded.

There is currently no file preview available, but this might change in the future.

## Wildcards
Only available in the default token configuration, this option let's you have a **randomized image** when you put down a certain kind of tokens. This is useful mostly for nameless NPCs, such as commoners in a tavern of perhaps some goblins you have with different fighting stances or color schemes to make it more immersive for your player than all identical tokens, and saving you the trouble of changing it in every unique token's settings.

To allow this, the path for the image must be set using a special path type ending with `*` (exact path format must be found to be posted, sorry).

## Token Size
The width and height values specified here are set to a number of grid squares (or hexes) and determine how much space the token takes on the field.
The scale slider only changes the image scale without changing the actual space taken by the token unit. A number higher than 1 results in a bigger image while a number below 1 makes it appear smaller.

# Position Tab
You should rarely need to use this tab, as all of these settings are generally used dynamically on the map or the [[Token HUD]].

## X & Y Coordinates
Pretty self explanatory, these are the coordinates of the token in pixels and are updated as you move the tokens around the map. You cannot manually update them with numbers. Do note that the coordinates cover a broader area than the actual map size, as there is a bit of padding around the edges to act as a "side table" area. As such, a token set to (0,0) won't actually be in the top left corner of the map, but rather some distance beyond that.

## Elevation
This does not have an incidence on the appearane of the token, but it does set how far "above" the map the token is (such as with flying creatures of ledges) and that number appears above the token if it is different from 0. It can be quickly adjusted via the [[Token HUD]], but it can be useful to set a default elevation for flying creatures.

## Rotation Controls
Again, the rotation field is greyed out and can only be changed on the map, using `Shift` (faster), or `Ctrl` (slower), + mousewheel to rotate the token, or by using `Shift` + `WASD` to make the token face the correct direction directly. The _Lock Rotation_ option is mainly useful for "portrait" style tokens that should not face a direction be instead stay upright.

A possible workaround, or **issue**, regarding the inability to manually change the token's rotation, lies with the default's configuration ability to "Assign" a token. If a default token is set in such a way, it will remember the rotation setting for future uses, which is not an issue with the coordinates since those are the ones you drag the token to when you put them on the map.