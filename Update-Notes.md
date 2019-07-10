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


