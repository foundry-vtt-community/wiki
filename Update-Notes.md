# Beta Version 0.3.X

## Beta Version 0.3.2, 2019-06-28

### New Features

* Added support for **Random Wildcard Tokens** which allows an Actor to be configured to support multiple token artworks and allows placed Tokens of that Actor type to randomly select from available token images when first placing a new Token instance of the Actor.
* Players with the "Trusted" permission level may now **configure their own Tokens** in addition to editing their Actor sheet. This can speed up set up and gameplay management activities for DMs who have trustworthy players.
* Added support for configurable **Folder Colors**. When editing a folder (via the right-click context menu) you may now select an optional color for the folder to help with organization. To remove a set color and return to the default appearance simply delete the color string from the form.
* Added a new integrated **Module Update** feature - this allows you to update installed modules to their latest version from directly within Foundry VTT. To update modules, visit the module management interface in the Settings Sidebar menu. The module update system is new and fairly limited at this time - but more improvements will be coming to make it even easier to load and maintain community-contributed content in the platform.
* The Token HUD which was first added in 0.3.0 has experienced continued improvements. The **Token Status Effects** menu has been moved out of the Canvas and into the HUD layer, featuring improved clarity and user experience.
* This update features a **Token Configuration Sheet redesign** which separates the Token config sheet into a smaller panel with multiple tabs. The Token Config sheet was getting very long and requiring vertical scrolling to work with. The new sheet separates Token Configuration into five thematic sections: Character, Image, Position, Vision, and Resources.
* Grid measurement distances of less than 1 unit are now allowed by the system which will help for maps where a single grid space is intended to represent a portion of a unit (like 0.25 miles).
* The limitation on Folder nesting depth has been relaxed for Journal Entry entities. **Journal Folders** may now nest up to 3 layers deep, and Journal Entries themselves are no longer required to be within a folder (they can just be in the base sidebar).
* Added support for new types of Compendium Packs, you can now created **Audio Playlist Compendia** and **Journal Entry Compendia** in addition to packs for Actors, Items, and Scenes.
* Improved the behavior of **Ambient Audio Easing** to now have a brief fade between volume levels when moving tokens. This avoids dramatic step-changes in volume and should make the auditory experience noticeably more pleasant. Furthermore, some logic improvements in related code has resolved a bug which could occur when multiple overlapping audio sources of the same type had different volume and easing preferences assigned.
* Modified the behavior of token visibility changes and their interaction with the combat tracker. Now changes to Token visibility will not also alter Combatant visibility on the tracker and the two settings are managed separately.
* Added a context option to Toggle Scene Navigation to scenes in the navigation bar context allowing them to be more efficiently removed from the top Navigation.
* Marking a combatant as **Defeated** in the Combat Tracker will now automatically apply a defeated icon as the Token overlay icon if the Token does not already have an overlay icon assigned. Which icon is used can be configued using `CONFIG.Token.defeatedIcon`.
* The **Canvas Pan Tool** has been deleted in favor of consolidating navigation workflows for canvas panning and token selection. I believe this makes a simpler and more consistent user experience, but I realize that some users who were accustomed to using the specific pan tool may not immediately love the change. The new UX is that right-click drag always will pan the camera for all tools and left click workflows are used for selection, movement, measurement, placement, and sizing.
* Added an explicit **Has Vision Checkbox** to the Token data model. Previously, whether or not a token had vision was inferred based on whether they had a non-zero value entered for dim or bright sight settings. This makes the workflow more explicit and allows for some simplifications when determining which tokens need to be tested for dynamic vision during gameplay. The "Has Vision" checkbox is located on the Vision tab of the Token Configuration sheet.
* Added a new convenience button to the sheet header for entities which are viewed directly from a Compendium Pack which allows for you to import the entity whose sheet you are currently viewing.
* Added a built-in workflow to support **deleting a World Compendium Pack**. Previously, world-level compendia which were created would need to be manually deleted and removed from the world.json file. There is now an automated in-app workflow to accomplish this - just be careful and read the warning message as any compendium content will be permanently removed.

### Core Bug Fixes

* Fixed a bug which caused movements to a wall endpoint while editing on the Walls Layer to temporarily display all door control icons.
* Identified an issue where the rich HTML content of TinyMCE editor fields was being included in every entity update instead of only when that content was modified by a user. Eliminating this issue has made entity update operations (for entities which have rich text fields) more efficient!
* Fixed a bad logical design for Token Deletion workflow which caused Combatants that represented that Token to be deleted after the Token request was processed, resulting in multiple overlapping and redundant DB calls.
* Aborting the placement of a Map Note by cancelling the creation dialog will no longer leave the preview pin visible on the Scene.
* Restored the highlighting of Scenes in the Navigation Bar to denote which scenes are publicly visible and which are GM Only.
* Added a `sort` attribute to the Folder data model in anticipation of upcoming changes which will allow folder sort order to be manually redefined.
* Fixed a bug with World Compendium creation which caused the incorrect file path to be printed in the world.json file, rendering the new compendium pack inoperable.
* Fixed a logic issue in the PIXI asset loader which allowed some event listeners to remain registered, potentially piling up over time.
* Resolved a situation in which releasing Token control could fail to hide an active Token HUD.
* Players should now experience an immediate change in the visibility of the local area if their own controlled token is hidden from play or revealed.
* Dragging minimized applications was incorrectly constrained by the size of the maximized application, preventing minimized apps from being dragged to the edges of the screen. This is now possible, if a minimized app is maximized into an out-of-bounds position, it's location is corrected to the closed valid location.
* Fixed another bug with Audio Playlists which could prevent playing tracks from beginning during live gameplay, instead requiring a browser refresh to begin playback.

### Core Software, APIs, and Module Development

* Added `FormApplication` support for a standard color-choice selector which will populate a defined text input field with a chosen color string. Use this pattern throughout FVTT where colors are chosen to allow users a way to provide a color string directly or remove an existing color choice.
* Modules and Systems may now provide HTML directly in their `description` field of their module.json or world.json manifest files.
* Added internationalization support with English translations for many additional Applications in FVTT: the Main Menu, the Settings Menu, and the Token Configuration Sheet.
* Renamed the main menu option from "Switch Player" to "Log Out" to be more clear about what will happen when that button is pressed.
* Altered the way that server-side database compaction is performed. Previously compaction occured for each table on a 10 minute interval regardless of what activity has occured on the server. To economize a bit more on compaction operations, the compaction process has been changed to occur once a certain threshold number of write operations have happened on a per-table basis. This results in fewer compactions and slightly improved performance.
* The `FormApplication` class can now support two new options - `submitOnClose` which will automatically submit the form if the window is closed and `submitOnUnfocus` which will automatically submit the form when an input element is changed and focus is shifted out of that element.
* Refactored the `ContextMenu` class to now accept an Array of menu items instead of an Object. The context menu will now automatically try to localize the names of menu items, if possible. The old-style Object of menu items is still supported, but a deprecation warning is shown and support will be removed in a future version (probably 0.4.0).
* Improved the behavior of the `getFiles` socket request to support returning a list of files and directories based on a glob-style wildcard path.

 
### D&D5e System Improvements

* Added fully configured Tokens for all CR0 monsters to the Monsters (SRD) Compendium.
* Added support to the Feat item type to track a limited number of uses per time period (short rest, long rest, day, etc...). The number of uses available is displayed next to the item name in the character sheet for convenient access and easier tracking of multiple resource types.
* Built a new **Special Traits** menu which is accessible on the Traits tab of the character sheet. The special traits tab allows for the configuration of specific features that mechanically alter the behavior of core 5e systems. Some feats are immediately supported and others will be added during future updates.
* Added support for the **Powerful Build** feat which will now correctly increase creature size for the purpose of computing encumbrance.
* Added support for the **Savage Attacks** feat which adds an extra weapon die when rolling critical damage.
* Added support for initiative-altering feats like Advantage to Initiative, Half-Proficiency Bonus, and the Alert Feat.
* Fixed a bug which prevented rolling of the NPC hit point formula.

## Beta Version 0.3.1, 2019-06-16

### New Features

* Implemented a major performance improvement for Fog of War rendering which is especially valuable for large scenes (10,000px and larger) which economizes substantially on the WebGL resources needed to render and save fog of war. This result in significantly improved application performance which is most noticeable for large and complex maps.
* Improve the specificity of the Scene Control application identification to allow for multiple scenes to be configured at the same time.
* Improve the flexibility of the placed Map Note pins to now allow them to be edited to reference a different Journal Entry after they were originally placed. Furthermore, this makes the system more fault tolerant whereby a map pin which points towards a non-existent Journal Entry no longer causes a failure for the notes layer.
* Usage of the newly added chat bubbles feature has been made more intentional - requiring the use of an explicit in-character `/ic` or emote `/em` message prefix. Default (non-prefixed) messages will no longer trigger a token chat bubble.
* Improved the render positioning for various follow-up applications which are rendered through the Actor Sheet. Now the Token Config, Sheet Config, and Portrait FilePicker apps will render in a more usable position relative to the actor sheet.
* Improve the rendering behavior of Sidebar Tab popout applications to allow their height to more dynamically adjust to changes in their inner content.
* Added a file locking mechanism to the Foundry VTT application which will ensure that only one currently running instance of the software is operating at a time within a single source directory. A consequence of this change is that if you want to host multiple worlds simultaneously on different ports, you will need to have multiple root directories for Foundry VTT to avoid any possibility of data conflicts. This is a limitation that can perhaps be relaxed in the future.
* Added a new core component to assist with Localization support. This allows for the core code, game systems, and user-defined modules to provide translation files which can add or extend support for different languages. The core software provides tools for defining translation tables and applying translations programmatically or during the template render process. I look forward to working with members of the community to gradually begin translating Foundry VTT into other languages! If you would like to sponsor a specific language translation, please don't hesitate to reach out to me in Discord.
* The newly added **Token HUD** has undergone some user experience improvements following feedback from the 0.3.0 release. Previously the HUD relied on a left click+hold workflow to trigger, but this has been moved to a simple right-click action to streamline and simplify the user experience.
* Change the styling rules for Actor and Item portraits in the sidebar to always show the top portion of an image. For asymmetric portrait style images, this reduces the odds that the actor will be "decapitated" in the sidebar thumbnail.
* Pausing the game will cause any in-progress token animation paths to end once the token reaches its next waypoint. This gives the GM more control over interrupting a movement to narrate certain key events which may happen as a result of the move.
* When placing wall endpoints you may now bypass snap-to-grid by holding the SHIFT key. This can be especially helpful when paired with wall chaining (CTRL) to create more circular wall shapes or for other special situations. Take extra care when placing walls which do not snap to the grid to avoid leaving gaps between your wall endpoints which could allow light to bleed through.

### Core Bug Fixes

* Fixed a bug which prevented Journal Entries from being shown to players with the image mode displayed as intended by the standard workflow.
* Fixed an issue with the FilePicker UI which prevented navigating upwards to the root public directory.
* Handle invalid user input in the attribute or elevation bar of the Token HUD. Previously an invalid input could result in the attribute bar getting nulled, now invalid user input will simply be ignored.
* A minor aesthetic improvement to the control icons for ambient light sources, sound sources, and placed measurement templates now positions the control icon more perfectly in the center of it's grid space.
* Fixed several bugs around audio playlist failures which could result in subsequent tracks in sequential or shuffled playlists from not triggering correctly for any or all players.
* Fixed a different playlist issue which prevented deleted Sounds within playlists from being properly removed for the triggering GM client.
* Tokens which have their combat tracker visibility set to hidden will now roll initiative using a private GM roll as originally intended.
* Make dynamic entity links in rich text fields failure tolerant. Previously if attempting to link to an entity which does not exist, substitution of that (and all other) entity links would fail.
* Fixed a client crash condition which could result when bulk Token deletion requests were made in a non-active Scene.
* Resolved a bug which caused chat messages that were sent without an active Scene to generate an error due to invalid speaker data.
* Improved the fog of war reset mechanism, which should no longer require two attempts in order to get fog to correctly reset to it's unexplored state.
* Background image filenames rendered via inline CSS in the sidebar are now wrapped in quotes to avoid common issues with file naming conventions.
* Entities where the default permission level was set to LIMITED were resulting in the GameMaster also having a limited view of the entity. This is no longer the case and GM permissions correctly override all others.
* Improved the rendering of long-named tokens in the combat log to avoid style breaks.
* Fixed a failure of World-level setting changes which prevented them from immediately propagating to other connected clients.
* Fixed an error where removing a token from combat using the right-click context menu did not always update that token's quick-controls display.
* Fixed a problem with the "Roll All NPC" button in the combat tracker which should now correctly roll initiative for all non-player characters.
* Fixed a bug with chat bubbles which could end up accidentally displaying a bubble for private whispered messages (whoops!).
* Improve the TAB token cycling workflow to avoid accidentally cycling tokens when a user is editing a form field.
* Fix a problem with the FilePicker for image type journal entries which prevented the picker UI from correctly rendering.
* Fixed an issue which prevented the Journal Entry from being properly resizable in either text or image mode.
* Removed an issue which attemped to place two walls with each click during wall chaining workflow, although the second wall was never placed due to zero length.
* Attempting to use the FilePicker for a file path which no longer exists will now correctly revert back to display the public root folder.
* Improve overflow scrolling for the ModuleManagement application to help with cases where users have many modules which could scroll off the viewable screen.

### Core Software, APIs, and Module Development

* Improved the behavior and layout of the Audio Playlist sidebar which should now behave more as expected when adding playlists and sounds. In particular, this update should resolve issues with players not having synchronized audio when the active track changes or was modified by the DM.
* Improve security around user-provided HTML input by sanitizing the set of allowed HTML tags more aggressively to strip any javascript which could be injected as inline HTML.
* Fixed a security loophole whereby players could assign themselves GM privileges using the provided API.
* Improve application security by refusing to serve database files directly via HTTP requests.
* Refactored the server-side Compendium code, making several key improvements for performance and reliability. The most prominent benefits for users involve bug fixes whereby compendium packs could get stuck in an unusable state when switching active worlds. Furthermore, newly created world-level compendium packs will be available for use immediately rather than requiring a VTT restart to function properly.
* Converted the hotkey shortcuts supported by the Electron layer to only function as local hotkeys when the application window has active focus. Furthermore, I solved the issue which prevented me from using F12 as a hotkey for the developer tools, so I have restored that original functionality to feature better consistency with browser behavior.
* Improved server-side validation of EmbeddedEntity update and delete operations to add an extra sanity check confirming that the requested item exists before attempting a delete operation, allowing for an earlier and more clear error message if unsuccessful.
* Increase the level of context provided to the Application.render function to allow for downstream applications to make more intelligent choices around what work to perform when render requests are received. Please see this issue for more detail: https://gitlab.com/foundrynet/foundryvtt/issues/951.
* The mechanism for triggering chat bubbles for sent messages has been made more direct - passing an optional flag through the socket creation event itself rather than simply inferring intent using the contents of the created message data.
* A second, but more minor performance improvement to Fog of War saving now allows this save operation to occur in the background rather than delaying the rendering of animations or vision updates.
* Made world migration operations slightly more tolerant -- previously a data validation failure experienced during a migration could prevent the migration completely leave a world in an un-launchable state unless the invalid data were manually removed.
* The previous update allowed for Modules to request a custom socket event to use for passing data between connected clients. It was an oversight to not extend the same level of functionality to game systems also. A game system may now have it's own dedicated messaging socket. Please see the following issue for usage details: https://gitlab.com/foundrynet/foundryvtt/issues/939
* Implemented an extra layer of precaution around the PIXI asset loader to prevent cases where attempting to load a video file (like .webm) with an invalid file path could cause the entire Scene load to fail as the attempted file load does not receive a rejected promise. More details in this issue: https://github.com/pixijs/pixi.js/issues/5336
* Implement a more graceful shutdown routine for active Worlds which are better protective of data and less prone to failure when switching between worlds.
* Improve the Electron initialization routine to ensure that it only attempts to load the local server URL after the Express server has correctly started listening for requests.
* Added an extra server-side safety check to ensure that a user has permission to upload files.
* Build the AWS SDK into the package as a dev dependency to help with building and distributing new versions and automating the upload and release process further.
* The `copyObjects` and `pasteObjects` methods in each `PlaceableLayer` will now return an Array of the objects which were copied or pasted when resolving their Promise.

### D&D5e System Improvements

* Added "adventuring items" to the D&D5e Items (SRD) Compendium. This expansion adds 100 pre-configured items as well as (perhaps more importantly) over 200 new pieces of licensed icon artwork which may be used to create homebrew items in your D&D5e worlds. Take a look at `public/systems/dnd5e/icons/inventory` for all the good new stuff! Also a special thanks to DoomRice from Discord who did some very helpful legwork to set up the set of items which should be added to the core compendium as part of this update.
* Added all Artisan Tools and Musical Instruments to the D&D5e Items (SRD) Compendium with pre-configured entries and accompanying artwork. Thanks very much to DoomRice from Discord who helped a lot with setting up these items for import.
* Completed the D&D5e Items SRD compendium with the remaining weapon and armor types which were previously missing.
* Began work on the D&D5e Classes and Class Features compendium packs which will eventually have all SRD class features available for convenient drag+drop use. Thanks to Thor's Wrath from Discord who has helped tremendously in setting up the data entries for this work so far.
* Improved the display if text edit fields in the Item Sheet to now be more legible in contrast to the sheet background color.
* Support creature size modifiers in the calculation for weight allowance and encumbrance.
* Added a new visual highlight cue for when a character exceeds 2/3 of their maximum encumbrance for players and groups which use optional rules in that situation.


