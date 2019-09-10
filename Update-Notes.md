- [Beta Version 0.3.6, 2019-09-10](#beta-version-036-2019-09-10)
- [Beta Version 0.3.5, 2019-08-20](#beta-version-035-2019-08-20)
- [Beta Version 0.3.4, 2019-07-31](#beta-version-034-2019-07-31)
- [Beta Version 0.3.3, 2019-07-17](#beta-version-033-2019-07-17)
- [Beta Version 0.3.2, 2019-06-28](#beta-version-032-2019-06-28)
- [Beta Version 0.3.1, 2019-06-16](#beta-version-031-2019-06-16)
- [Beta Version 0.3.0, 2019-05-29](#beta-version-030-2019-05-29)

# Beta Version 0.3.X

## Beta Version 0.3.6, 2019-09-10

Greetings friends. I'm proud to share a new Foundry Virtual Tabletop beta update. This update has some major and substantial updates to core systems and software - focusing on improving the stability and consistency of key systems. The biggest improvement in this update is the new redesigned Configuration and Setup experience which gives a centralized management panel for Systems, Modules, Worlds, and core VTT software updates. The experience for installing and updating new community content has never been easier. In addition to this major new feature, there are a ton of quality of life improvements and bug fixes designed to smooth out some of the rough edges introduced in previous updates. 

I am proud of this set of changes and know it will serve me well as I continue development of new tools and functions looking ahead towards 0.3.7. Thank you all for your continued encouragement and sharing of this project - your help in spreading the word and supporting my work means so much to me.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- Implemented a major new feature which redesigns the *Configuration and Setup* page of Foundry VTT. This new page is far more powerful and functionality rich. From this centralized landing page you can update the core software, install and update Game Systems, install and update Modules, and create and manage Worlds. Systems and Modules can be installed directly with one-click by providing a link to their manifest (module.json or system.json) file. Installed Systems and Modules can be easily and automatically checked for updates and updated if a new version is available. I am very excited for this change as I believe it will make the process of installing and managing community created content much easier in Foundry VTT, further empowering the awesome module and system developers who are hard at work in the community.
- Redesigned the Game Settings menu to support separate tabs for Core, System, and Module settings while sorting the displayed modules alphabetically for improved organization.
- Due to the introduction of the new Configuration and Setup page which handles Module installation and updates, the ability to update Modules while inside an active World has been removed. This is a good change, as updating modules "in flight" caused some problems and complexitities which were not always well handled. You still configure which Modules are active within a World using the same Manage Modules application as before.
- The display of Tokens on Hexagonal Grids has been improved so the bounding box for the token mirrors the hex dimension, instead of being too wide or too tall for the shorter side of the hex.
- Files and Folders displayed in the File Picker will now be sorted alphabetically in a case-insensitive way. Previously lowercase names were sorted after uppercase ones (per Unix convention).
- Formatting of the exported text chat log file has been improved to add more detail about dice rolls, showing both the initial formula, and the rolled result (including all rolled dice).
- Incorporated localization support for the Scene Configuration sheet. Thanks to Ayan for contributing an updated HTML template and translation string keys.
- Improved the sorting logic for Combatants, adding an additional sorting layer after initiative score and name for the Token ID to ensure that the resulting sort order is always deterministic.
- You may now include some additional flavor text along with any dice roll submitted in the chat window by separating the roll portion of the command with a # character. For example /roll 4d6kh # Rolling for ability scores!.
- Added additional buttons to the Settings sidebar as an alternative way to return to key setup menu screens. There are new buttons for "Return to Setup", "Configure Players", and "Log Out".
- Added a new button on the Settings tab of the sidebar to render the Community Wiki documentation in a pop-out iframe. Many thanks to errational, CyberPathogen, and the many other wonderful curators and contributors of the community wiki for creating this helpful resource.
- The ability to export-to-JSON and import-from-JSON has been added for more Entity types - including Items, Journal Entries, and Scenes. Previously only Actors had this capability.
- Added localization support for context-menu options on Sidebar Directory containers.
- Added a new Journal Entry context menu option to Duplicate an existing entry, as was possible for other Entity types.
- Improve the hit area definition of newly added Drawings from the 0.3.5 update so they are easier to select and manipulate once drawn.
- Made a change which allows chat commands to span multiple lines without being incorrectly truncated.
- Users who have "Limited" permission to a Journal Entry will now be able to see Map Notes placed for that entry, but will not be able to inspect the details of the note. This can allow GMs an alternative option for label significant locations without revealing details about those locations to players or needing to keep those details in a separate entry.
- A User's chosen color is now shown as a border around all out of character chat messages sent by that User.
- The syntax for sending whispered messages in chat has been made more flexible to support /w and /whisper prefixes in addition to the previous @User syntax.
- Web URLs posted in chat messages will be automatically converted to a clickable hyperlink.

### Core Bug Fixes

- Fixed an issue with attempting to add an Owned Item directly to an Item type compendium.
- Changing the Actor that a Token references would not fully take effect until a hard refresh, as double-clicking the Token would continue to open the old Actor's sheet.
- Fixed a problem with IP address identification which sometimes resulted in the local and internet IPs not being properly displayed.
- Solved a problem for newly created Actors which prevented the img attribute from being initially present in their prototype Token data model.
- Hardened a loophole with EULA acceptance which previously allowed you to simply close the window to dismiss the agreement without later prompting.
- Applied a fix for the PIXI v5 update which caused a vertex buffer overflow when rendering large Graphics objects (like big Hex grids). This caused hexagonal grids to no longer render after some number of polygons.
- Fixed a problem that occured when deleting a World-level compendium pack which had not yet connected to its database.
- Removed visibility of the "Delete All" button on the Measured Templates layer for players who could not use that button as they lack GM permission.
- Made a change to lock tiles while they are in the middle of a drag workflow. Previously the Tile could be rotated via mousewheel while mid-drag causing server desynchronization problems.
- Applied an additional check to prevent Compendium pack paths from being written to world files as absolute paths instead of relative to the World directory as intented.
- Fixed an issue since the PIXI v5 migration which prevented Scene background color from being properly applied.
- Corrected the rendering of large hex grids in 0.3.5 which produced an incorrect offset with artifact lines.
- Improve the vertical spacing of TinyMCE editors since the v4.x update in 0.3.5 to make better use of the bounding container.
- Fixed an order-of-operations problem with the unregisterSheet method which caused it to incorrectly clear a previously registered sheet for all Entity types, even if a specific type of entity to no longer use the sheet for was specified.
- Improved the logic of the version comparison function used to detect module and system update availability to work for more types of versioning schema.
- Fixed a bug in the "Simple Worldbuilding" system which prevented Owned Items from being properly editable.
- An unintentional "feature" in 0.3.5 caused mousing over a Polygon point during a drawing creation workflow to undo that point. This, while sometimes nice, was an unintentional workflow that could sometimes produce frustrating results and has been removed.
- Fixed a bug whereby an Owned Item could be dropped on the Actor who owns it, thereby duplicating the item data in that Actor.
- Drawing objects can no longer have no line, no fill, and no text - causing them to become effectively invisible. Drawings must have at least one of these values set.
- Remove the "Delete All" button from Players on the Drawing layer since they do not have GM permission to delete the drawings of others. This was a bug fix for now, but I may bring this back in the future where the button would only delete drawings belonging to the user.
- Corrected accidental residual references to CONFIG.Token which has been removed in favor of other global configurations.
- Improved the approach towards regex matching for chat message whispers and dynamic entity links to better support international characters in Firefox where unicode regex escapes are not supported.

### Core Software, APIs, and Module Development

- The server-side implementations of "Pakcages": System, Module, and World have all been jointly refactored to extend the same abstract base Package interface and share much more common code and implementation. This has improved quality and consistency of how these packages are managed and described within the VTT software.
- Broadly refactored and improved code quality for the Chat Log sidebar and the messages that are rendered within it. This was some of the oldest FVTT code, as chat was one of the first features I implemented. It was well overdue for a fresh coat of paint.
- Refactored the sidebar directory templates and CSS rules to adopt a flexbox layout which should be more friendly for mod developers who want to add additional content into the sidebar.
- The ChatMessage Entity now has a required type field added to its data model to more explicitly differentiate different types of chat communication. The valid types of chat messages are enumerated in CHAT_MESSAGE_TYPES.
- Some changes to keystroke handling have been implemented. Several keys were previously only captured on keyup, which are now captured on keydown with a repetition filter added. This provides a more responsive experience when interacting with these controls.
- Performed some code cleanup in the Combat class to remove some deprecated properties and bring greater consistency to the structure for current and previous round tracking.
- Improved the informativeness of the error message thrown if the --world startup flag references a World which does not exist.
- An informative fatal error is now triggered if there are multiple packages (systems, modules, worlds) which have the same "name" attribute in their manifest files.
- A new structure is supported (and enforced) for defining module-based translation files. Under this new approach, languages are defined as an Array of Objects, and JavaScript code is no longer required to manipulate the CONFIG object as this is handled automatically. See this [issue on GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1342) for more details.
- English language translations are now always used as a fallback option for any localization strings which do not have an available translation in the designated preferred locale.
- Because of the new management strategy for module-provided translation files, these translations are now accessible on the main configuration and setup pages of the Application where modules were previously not able to contribute content.
- Improved server-side zip file extraction to support an option to de-dupe the folder structure during the extraction process if nested directories are present.
- Added a confirmDialog() helper function to streamline the process of rendering standard yes/no prompts using less code.
- Revisit support for options.height = "auto" to be specified in an Application render options - auto height applications will be automatically resized (vertically) when they ar re-rendered to accomodate changes to the internal content.
- Improve server-side Socket management to automatically learn the Entity class names for which to open socket listeners instead of hard-coding them.
- Added a very simple Number.isNumeric() helper method to test whether a string represents a numeric value.
- Enforce a safe Proxy environment for evaluating math expressions in dice rolls. Thanks KaKaRoTo for pointing out this cool approach towards evaluating code using a limited and controlled scope.

### D&D5e System Improvements

- Stat blocks and actions for CR 1/4 monster compendium entries have been added. Token artwork and biographies for these creatures are still pending, but I want to push ahead on making sure the SRD Monsters compendium has usable creature definitions for running encounters. Expect further progress in this area on an ongoing basis.
- Right clicking a skill proficiency icon will cycle backwards in addition to left click cycling forwards. Thanks Giddy for the suggestion.
- Added support for a custom weapon attack critical threshold configured as an additional special Actor trait. Thanks TimPosney for the suggestion.
- Updated the character sheet to display the effective Initiative modifier (after additional bonuses) instead of just the base modifier. Thanks to RedReign for the suggestion.
- Added equipped, attuned, and rarity fields to every item type in the 5e system data model.
- Minor tweaks to the content displayed in the footer of spell cards.
- Fixed a bug with the "apply damage" chat dropdown which was incorrectly setting current HP to undefined instead of applying the relative damage difference correctly.
- Ensured that all Spells in the 5e Spells compendium have the "prepared" attribute present in their data model (with a default value of false).

## Beta Version 0.3.5, 2019-08-20

Hello tabletop friends! Foundry Virtual Tabletop update 0.3.5 is here with a fresh round of feature enhancements, bug fixes, and underlying software and API improvements. The centerpiece of this update is a major new system for Foundry Virtual Tabletop with the addition of Drawing Tools which allow for improvised freehand sketching or shapes which can be highly customized with line, fill, and text styles. Additionally, this update adds improvements to the Item Sheet API, and new features for the Combat Tracker, Measured Templates, as well as a host of bug fixes and minor improvements.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. Stay tuned in the next couple days for an additional post sharing some reflection on the past year and plans for the official product release. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- The addition of Drawing Tools is a major milestone for Foundry Virtual Tabletop, as this was one of the few outstanding systems that is critical to support for a modern VTT. I would like to thank all the testers and community members who have been exceptionally patient with me while I reluctantly dragged my heels on tackling this major feature. I would also especially like to thank KaKaRoTo who did some extremely useful prototyping and was a helpful collaborator while I worked through the implementation of this system. Please thank him if you see him in Discord and be sure to support his other exciting FVTT related projects.
- Drawing Tools are a new layer of the game canvas, positioned above the Background and Tiles, but just below the Grid and other placeable objects. Four types of drawings are supported: rectangle, ellipse, polygon, and freehand. Each drawing can be created, transformed, and independently configured. Drawing data is vectorized for efficient storage and flexibility.
- Added a Drawing configuration sheet to fine-tune the properties of your drawings - customize the line art, fill color or texture, and overlay text for each drawing. Additionally, clicking the gear icon in the scene controls allows you to customize the default drawing setup for any future artwork.
- Added a Drawing HUD activated via right-click on a placed drawing which can control the visibility and locked state of the drawing as well as adjust its z-index sorting. More on this in the following point.
- Added support for z-index sorting of Drawings and Tiles. This allows you to customize which objects are rendered above or below others to control layering when using many tiles or drawings. Shifting the z-index of a Drawing or Tile is available through it's HUD controls activated on right-click.
- Updated the core software to PIXI version 5. This is a major release with some very significant long run benefits for the project. I'm really excited about this update as it unlocks the potential of WebGL2 that will be applied in more places, providing continued performance improvements as well as substantially added flexibility for Graphics geometry - which is already taken advantage of within the new Drawing tools. For those of you whom are interested in the underlying technology, you can read more about the new PIXI major version here: [https://medium.com/goodboy-digital/pixijs-v5-lands-5e112d84e510](https://medium.com/goodboy-digital/pixijs-v5-lands-5e112d84e510)
- Migrated the core software to upgrade to the TinyMCE 5.x editor which includes several bug fixes and a more streamlined UI.
- Migrated the application nativization layer to Electron 6.0. This is an optional update that will eventually roll out to all users but is available immediately for anyone who downloads a fresh version of FVTT. The Electron application is not updated through the internal auto-updater, so if you want to get the latest Electron build of the Foundry Virtual Tabletop app, you can consider re-downloading a new full version. There are no meaningful benefits at this time aside from general modernization.
- Item Sheets can now be configured on a per-type and per-entity basis the same way that Actor sheets can be configured and overridden. This allows for modules to define custom Item sheets which only are used for a specific Item type (like a Spell, or a Weapon) while individual items can change the sheet type used for that particular item. I am excited to see how this new level of flexibility for displaying Item sheets generates a new wave of creations and ideas from the modding community.
- Improved the UX around token dragging for tokens larger than 1x1 base. Previously some visually inconsistent results could occur where the preview "shadow" token and the true final position of the Token once dropped were inconsistent.
- Whisper message targets are now regex matched in a case-insensitive way with added support for special unicode or foreign characters allowing for more broad and consistent coverage of private chat messages.
- Added a Combat Tracker configuration option to automatically skip defeated combatants in the turn order. This option can be turned on by clicking the gear icon at the top of the tracker. Defeated combatants will only be skipped when moving forward in the turn order, you can still go backwards to return to a skipped combatant.
- Added internationalization string translations for Scene Controls and Tools.
- Holding the ALT key while pasting (CTRL+V) copied Tokens will result in those Tokens being created in an initially hidden state the same way that holding ALT during a drag+drop Token creation creates a hidden token.
- Added a distance tooltip text to Measured Templates which clearly states the distance of effect for the placed template both during the creation process as well as whenever you switch back to the Measured Templates layer in the Scene Controls.
- The vertical scrolling position of all Sidebar containers are now remembered, so that when a sidebar is re-rendered your previous scrolling position will be automatically restored, creating a more smooth user experience.

### Core Bug Fixes

- Fixed a somewhat rare but serious edge case failure with Token vision and wall collision which could occasionally allow tokens to see or move through walls when those walls perfectly bisected the diagonal of a grid square and the Token was approaching that bisecting wall from a particular direction of movement.
- Resolved a significant problem with movement of non-player tokens which would result in the visibility state of the token not being updated when it moved into or out of field-of-view for the player token.
- Fixed a bug with socket listeners for world Setting changes which were incorrectly double-parsing JSON content of the settings and potentially triggering errors in some situations.
- Fixed a rendering problem with MeasuredTemplate objects which would cause the grid highlighting to often become completely wrong when the template was re-painted.
- Corrected a bug which could sometimes incorrectly require the use of brackets around names for whispered chat messages even if the target name was a single recipient without any spaces in their user or character name.
- The user-provided update key is now trimmed of leading or trailing white space to avoid a common pitfall that several users have encountered while updating to a new version.
- Special characters are now supported in dynamic entity links, allowing for more reliable linking of content - especially in foreign languages.
- Improved some failure modes around wildcard patterns for random token artwork. Note that while some failure modes were addressed, there is still a known failure which arises for Windows users when the wildcard path contains bracket characters. This is due to a bug in an upstream parsing package for which there is no current workaround. I strongly recommend avoiding brackets in file paths for VTT content as they are not web-compliant and will be a likely source of trouble.
- Fixed a bug which could prevent module registered settings from being properly configurable within the Configure Settings menu.
- Corrected some errors for the Microsoft Edge browser resulting from implicit catch blocks which are not supported by the Edge spec.
- A bug when unlocking or locking doors could incorrectly cause the wall highlight to be shown temporarily. This no longer occurs.
- Prevented a failure mode through which dice rolls for Tokens without a valid referenced Actor would fail rather than evaluating against an empty data object.
- Corrected a problem with the Roll.alter() method which was not properly altering the contents of a Roll object because of changes to the initialiation process for Rolls.
- Fixed a problem which could lead to the loss of content from a TinyMCE editor when the user followed a certain workflow that resulted in the app re-rendering during the midst of saving edits.
- Prevented a failure when copying Items from a synthetic Token sheet that prevented those items from being appropriately named in their transferred data.
- Refactored the Entity Sheet registration process to generalize across any arbitrary number of Entity types. These improvements were in support of the configurable Item Sheet changes referenced above.

### Core Software, APIs, and Module Development

- **Breaking Change**: Support for glob-style inclusion of static scripts and styles in modules and systems has been deprecated, effective immediately. I apologize to any community developers who are impacted by this change, however the number of potential edge cases that users can experience from inconsistent glob pattern parsing for different root paths of Foundry Virtual Tabletop can make errors which occur as a result of glob parsing extremely difficult to reproduce or track down. Having seen some of these issues come up, I have decided it is better to rely upon explicit file paths for script and style inclusion rather than pattern matches. Please update your module.json or system.json files accordingly if you were previously using a glob-style pattern to include static content.
- Continued work to expand the coverage of server-side data validations when new data is written or updated in the database. These additional validation checks help to assert the data quality that is entered, avoiding potential future bugs. Several new checks have been added for core entity types as well as to many attributes for placeable objects which were previously optional and now are required and validated.
- Improved the logic used to initialize the game session when the window is first loaded to avoid possible race conditions between DOM initialization and JavaScript loading.
- The server-side System object has been refactored to improve it's usefulness and avoid needlessly exposing server-side file paths to clients when the System data is serialized for vending to the connected user.
- Added a boolean flag to each module in game.modules to denote whether or not that module is currently active in the World.
- Implemented a performance improvement to the rectangular select tool to enable it to reduce the number of object control or release operations required to only operate against the differential set instead of against all selected objects.
- Added support for a new "button" type scene control in addition to tools and toggles. Button type controls will fire their callback once clicked, but not become an active tool.

### D&D5e System Improvements

- The complete set of CR 1/8 monsters supported under the OGL has been fully configured for use in the Monsters SRD compendium complete with beautiful Token artwork from Stryxin and Forgotten Adventures and custom creature biographies courtesy of Penelope (Vyrnali). Thank you both so much for your fantastic contributions to the D&D5e system!
- Fixed a bug with consumable Item sheets in the 5e system which prevented the maximum number of charges from being editable.
- Added a standalone Gulp script to the 5e codebase for building the JavaScript and CSS distributables.
- Newly created Items in the D&D5e system will have an empty string as their description instead of undefined.
- Fixed a pathing issue for D&D5e system compendium packs which was initially introduced (and later hotfixed) with the 0.3.4 release.

## Beta Version 0.3.4, 2019-07-31

Hello tabletop friends! Foundry Virtual Tabletop update 0.3.4 is here with a fresh round of feature enhancements, bug fixes, and underlying software and API improvements. This update is pretty substantial and addresses a large number of bugs while adding functionality to better empower modders and system developers. Highlight new features in 0.3.4 include *Sidebar Search*, chat support for *Entity Links*, and the addition of the commercially licensed *GSAP Library* for animation.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

* Sidebar directories for Actors, Items, Scenes, and Journal Entries now have a filter and search bar at the top of the sidebar which allows you to quickly find entities by name. The filtering logic is case insensitive, and deleting a filter will restore the sidebar to displaying the full set of results.
* Dynamic entity links can now work in chat messages. This allows you to "mention" certain Actors, Items, Journal Entries, or Scenes in chat. For example "Hi @Actor[Bob]".
* The context menu for Journal Entries in the sidebar now features a new option to *Jump to Pin* which is available if that Journal Entry is pinned to the currently viewed scene. Using this option will pan the Scene view to highlight the location of the map Note. Many thanks to *Moerill* from Discord for inspiring this feature.
* The fog of war opacity settings have been adjusted for GM users to preserve some limited visibility of the map while still differentiating areas which represent unexplored fog of war. Many thanks to *trdischat* on Discord for his helpful module which motivated this change.
* Foundry Virtual Tabletop now includes a paid commercial use license for the Greensock (GSAP) animation libraries (https://greensock.com/) within the core platform as well as any downstream systems or modules! GSAP modules can be added by any module or system by requesting the inclusion of these scripts in a module or system manifest file.
* Newly created Users will each receive a randomly selected color to differentiate them. Colors can still be manually changed at any time, but this will help to differentiate users by default.
* Provide a GM-only context menu option to permanently delete a Folder AND all of it's contained subfolders or entities. Please be cautious in using this option, as the operation is not recoverable, but the power is in your hands.
* Hovering over a Token which is an active Combatant in the tracked Combat Encounter will now highlight the combatant. This helps to easily answer questions like "when is it this Goblin's turn?".
* Game systems may now designate an attribute from their Actor data model which is used as the default tracked resource bar for Tokens.

### Core Bug Fixes

* Solved a long-standing problem which prevented the use of large (15MB+) audio files in Foundry VTT. Improvements in the upstream Howler library have now allowed me to move to HTML5 audio streaming which supports such large files in a more more performant way. This change also reduces the initial load time between when an audio request is made and when playback begins. Thanks to *KaKaRoTo* from Discord for identifying that this change was now possible.
* Correct a bug with module-provided localization/translation files where the system was looking for module translation files in the incorrect data path.
* Addressed a bug which caused Tile object deletion to not deactivate the Tile HUD if it was displayed for the deleted Tile.
* Closed a loophole which prevented the Combat Tracker from rendering if some Combatants represented Tokens which have no valid Actor.
* Holding the ALT key was incorrectly highlighting the borders of placed Tile objects when the Tiles Layer was not active. This has been corrected.
* Fixed problems occuring when Tile objects were resized by very small amounts or collapsed upon their origin point.
* Disabled the resizing handle for Tile objects which were set to the locked state.
* Avoid needlessly opening a new tab for links which directly refereence a `javascript:void(0)` call.
* Fixed a problem related to updating the Permission settings for Actors which do not have any active tokens placed which represent them.
* An edge case for Scene data resulted in a Scene which was flagged as Active, but not shown in Navigation. This logic has been hardened to guarantee that Scenes are inactive when removed from the navigation bar.
* A flaw in the layer deactivation logic caused highlighting for selected Wall objects to remain visible when the Walls Layer was deactivated - this no longer occurs.
* Fixed an issue with Wall endpoint editing which could result in the Wall being continuously selected and de-selected without triggering the Wall Configuration sheet.
* Resolved an issue with MP4 video assets in Scene backgrounds, Tiles, or Tokens which was incorrectly blocking the file extension from being used.
* Avoid displaying an Actor context menu option to showcase Token artwork if the Actor's prototype token does not have any image file defined.
* Restored hover tooltip strings for parent Tool categories in the Scene Controls interface element.
* Changing the file path of an Ambient Sound object placed in a Scene now will immediately alter the audio effect being played, which previously required a hard refresh to take effect.
* Fixed an issue with the newly added Compendium Update API methods which failed to adequately validate user permissions when making changes.
* Solved a race condition in the Combat Tracker which could result in infinite recursion when multiple changes for the same combatant occured simultaneously.
* Corrected a bug which blocked changes to an Actor's prototype token from being properly saved to the database.
* Fixed a bug in the World Selection interface that could, in some cases, lead to the World's text description to be lost.
* Strengthened the validation around the serialized Roll object contained in Chat Messages to avoid situations in which the Chat sidebar could not be rendered.
* Improved the behavior Application header buttons which prevent them from also doubling as drag handles.

### Core Software, APIs, and Module Development

* Standardized the way that static files (styles, scripts) are loaded for Systems and Modules.
* Modules and systems may request that common scripts, like those offered by the new Greensock libraries, be included. Scripts requested in a system or module manifest will look first for matching files relative to the module root while falling back to the contents of the `public/scripts` folder. See the [issue in GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1208) for more details.
* The `combat._previous` Array which reported the prior round, turn, and tokenId of the combat encounter has been converted to an Object `combat.previous` with named keys. The `_previous` attribute can still be used, but will be deprecated in a future version.
* Added server-side data validations for Token width and height attributes, requiring them to be positive numbers.
* Implemented several public methods for common Application manipulations including minimization, maximization, sidebar tab switching, and sidebar collapse toggling. See the [issue in GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1193) for more details.
* Additional Hook events have been added for when a PlaceableObject enters or exists a hovered or controlled state. Please see the [issue in GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1181) for more details and usage examples.
* Improved upon the security of dice Roll result evaluation to avoid execution of functional code.
* Refactored the way that Collection and SidebarDirectory tabs are rendered in order to standardize and reuse more code between Applications.
* Standardized the the URI encoding conventions used in the FilePicker and the server side Files object.
* Modules and Game Systems may now deisgnate in their manifest files that they depend on a minimum core VTT version in order to function properly. Please see the [issue in GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1097) for more details.

### D&D5e System Improvements

* The D&D5e system specified some rules for `<span>` elements which forced them to be displayed as block elements. These rules have been relaxed so that span elements remain naturally inline.
* Added support for automatic recovery of feat uses per Long Rest or Short Rest. Thanks very much to *Felix* from Discord for submitting this improvement to the 5e codebase.
* Added support for a global saving throw bonus, for example from a Ring of Protection or from a Paladin Aura. Thanks very much to *tposney* for submitting this improvement.

## Beta Version 0.3.3, 2019-07-17

Hey everyone, it's time for another exciting Foundry Virtual Tabletop beta update, with version `0.3.3` that adds a huge number of new features and bug-fixes. With 70 issues addressed in this update it is a new record for the largest update (in terms of issue count) ever! This update includes some big new features like Token Actor Data Extension, support for Universal Plug-and-Play which removes the need for port forwarding, group editing for Wall objects, addition of the initial system for Weather Effects, and server-side storage for Fog of War exploration. These major feature improvements are partnered with a lot of helpful bug fixes and API improvements.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

* This update adds support for *Token Actor Data Extensions* which allow any token, even one which is not linked to a base Actor entity, to have it's data model updated. This allows for some really amazing possibilities, like having Tokens whose statistics, items, or abilities are randomized at the time of the Token being placed. Double clicking a Token will continue to open an Actor Sheet for that token, changes to this sheet are applied as Token actor-data overrides if the Token is not linked to the actor directly. Furthermore, this change allows for Token-specific resource bars to be deprecated and removed from the Token data model. The attribute bars displayed for Tokens now refer directly to that Token's actor data. This is a powerful change, but it adds a several new complexities or situations that developers may encounter. Furthermore, the relationship between Tokens and Actors has historically been confusing to users - so more work will certainly be required to ensure that Game-Masters can easily understand the system.
* Automatic support for [Universal Plug-and-Play (UPnP)](https://en.wikipedia.org/wiki/Universal_Plug_and_Play) has been added to Foundry Virtual Tabletop. If your local network allows for UPnP, this means that you no longer need to deal with Port Forwarding in order to allow others to connect to your game! Sincere thanks to KaKaRoTo for helping to demonstrate this proof of concept and advocating for this improvement. I believe it will provide a big benefit for new users who are discovering the software and are uncomfortable with the challenges of port forwarding.
* Added support for *group editing of Wall objects* which allows you to select multiple walls and edit or delete them as a chained sequence. Clicking on a Wall while on the Walls Layer will select the wall. Holding SHIFT while clicking walls will add or remove walls from the controlled set. Holding ALT while clicking on a wall will select all Walls which belong to the chained set of linked endpoints. Double-clicking a wall endpoint while a set of walls are controlled will allow you to edit the properties of all Walls with a single update, for example, if you want to switch a set of existing walls to be invisible or terrain typed.
* Added the first implementation of *Weather Effects* with support for Rain, Snow, and Autumn Leaves weather effects. More weather effect types and variable settings for each effect type will be coming in a future update, but I'm very excited to add this initial functionality for testing as a proof-of-concept.
* Fog of War exploration now features *server-side persistence*. Previously fog data was stored client-side per User. This could fail if the User connected on different devices or reset their browser cache. Now fog exploration data is stored as part of the World data, protecting players from data loss in fog exploration progress.
* Added a new Tile HUD which mirrors the behavior and functionality of the Token HUD for controlling Tile visiblity settings. Right clicking upon a Tile (while on the Tiles Layer) will activate the HUD for controlling that Tile.
* Tile objects can now be *locked in place *to prevent them from being accidentally modified or moved. The conntrol to lock or unlock a Tile is available in the Tile HUD.
* The styling and performance of the World Setup page has been improved to load data asynchronously to speed up the process of browsing and editing World information before a game is started. Each World can now be assigned a *World Banner Image* which can be used to provide additional visual flair to each world. This world banner will be reused in other places in the future.
* A toggled mode has been added to the Canvas Notes Layer which allows for *Map Notes to remain visible* and interactable while on the Token layer. This can be ideal for maps where exploration and reference of key points of interest plays an important role. There is not yet a way to store this setting in a persistent way, but this will be added in a future update.
* Added a visual toggle to *collapse the sidebar* to a minimal version only containing the tab buttons (which can still be right-clicked to pop them out). This can be a great way to keep the UI clean when not in use to focus on the game canvas.
* The position and zoom level of the camera in a Scene will now be remembed, so that re-rendering of the Canvas due to settings changes will now cause the camera to reset back to a default position, instead it will now stay fixed in its previous location for a more smooth user experience.
* Added localization support for the Wall Configuration sheet.
* Added support for WebP as a valid and supported image file format.
* When selecting an audio file for a Sound track in a Playlist, the title for the track will be automatically populated using the selected file name if a name has not been otherwise set.
* Generalized the behavior of the rectangular select tool to now work with all PlaceableObject layers. This tool is currently only enabled for Tokens and Tiles, but the underlying functionality to support rectangular selection for other PlaceableObjects is now possible and will be added in a subsequent update.

### Core Bug Fixes

* Resolved a serious problem with Measured Template grid highlighting which neglected to account for the amount of distance represented by each grid square, resulting in an exponential increase in computation for large template sizes.
* Fixed a bug whereby tokens which collided with a Wall during a groupwise Token movement would be rocketed towards the top-left of the Canvas instead of having their movement stopped.
* Corrected an issue with whispered messages where spaces in a player name prevented the whisper from being sent.
* Dice rolling will now accept a capital 'D' for the number of dice rolled, for example `/r 4D6` and `/r 4d6` are equivalent.
* Fixed an issue which sometimes prevented Token vision from being correctly initialized when the page is first loaded due to an asynchronous behavior which was not properly resolving before downstream steps were triggered.
* The Combat Tracker sidebar UI was incorrectly treating initiative rolls of zero as an indication that the combatant has not yet rolled initiative. This is now resolved and a result of zero is allowed, despite being highly unfortunate.
* Fixed a bug in the Simple Worldbuilding system which threw a fatal error when the Sheet Configuration UI was activated.
* Changing the visibility permission for Compendium Packs was not applying immediately for other connected players, this has been corrected.
* An issue with the new in-app World Compendium deletion logic caused it to be (accidentally) restored if re-created with the same name during the same session. Now deleting a World Compendium is, actually, permanent.
* Fixed a failure which could occur during World migration where a compendium pack was not connected before an attempted migration was applied.
* An issue in the Sound CRUD workflow which failed to provide the parent Playlist ID to the socket event has been fixed.
* Prevented a failure in the Combat Tracker which caused the "Reset Initiative" button to break the functionality of the app.
* The file paths returned by the server using it's client-side file paths transformer will now always return URI encoded paths.
* A bug in the Player Configuration view caused a new User to be created when the Enter key was pressed in an input field instead of submitting the form to update changed users.
* Fixed a bug which prevented the new TokenConfig sheet from rendering if a Token no longer references a valid and existing Actor.
* Closed a loophole which caused ChatMessage entities which contain Roll objects to render their HTML content twice, once in the toMessage function and again in the main `ChatMessage.render` call.
* Corrected an error which prevented the main menu (ESC) from being rendered after a ContextMenu was closed and destroyed.
* Fixed a bug which accidentally allowed a Token with `hasVision` enabled but zero distane assigned to it's vision settings could incorrectly reveal the entire map Fog of War as was the behavior for GM users prior to the addition of this checkbox.
* A problem with Tile objects could cause strange and unpredictable results when resizing them using the drag handler, flipping the tile aspect ratio or size. This has been addressed and the resizing process for tiles should now work in an intuitive way.
* Fixed a problem that could cause the Chat Log to become unloadable if it contained a message which was originally posted by a User who has since been deleted.
* Corrected a defect with the volume sliders for Playlist audio which allowed players to change the default volume level played for all players instead of (as intended) only locally overriding their own playback volume.
* A bug could allow Players (non-GM) to move the position of Tiles, a permission which should only be allowed to GM users.
* Improved the Canvas initialization behavior to eliminate a problem which could occur where the aspect ratio of the viewport changed while the Canvas was being rendered. A redundant check at the end of the drawing process looks to see whether the dimensions changed while drawing.
* In some situations, status effects applied to a Token do not show up immediately for a Combatant in the Combat Tracker. This has been more reliable, so that applied status effects will appear immediately in the Tracker.
* Clicking on a combatant in the tracker will no longer attempt to pan the map to that Token's location if the user is not viewing the Scene in which the Combat Encounter occurs.
* Fixed an issue with the `_activateEditor` function in a FormApplication which could cause it to be fired before the HTML of the application was ready for use.
* A minimized ActorSheet would incorrectly attempt to re-render itself as maximized when a portion of the Actor data is changed. Instead this update will now happen in the background and leave the application minimized.
* Fixed a resource contention issue which could cause icons from Token status effects to become unusable depending on the load order of the PIXI Canvas.

### Core Software, APIs, and Module Development

* Refactored the event names used for Compendium operations to better standardize their design with other CRUD or GET workflows.
* The signatures used for Hooks which interact with Entity and EmbeddedEntity CRUD workflows have been updated and made more consistent in terms of their naming conventions and the arguments which they transact. Please see [This Issue](https://gitlab.com/foundrynet/foundryvtt/issues/1131) for documentation and examples of how hooks (and pre-hooks) work after this update. Please note, in particular, that update-type operations now also provide the differential data object as an argument to the hook, allowing the user to see exactly what data was changed.
* The `setProperty` utility function will now assign Array elements by positional index if the parent object is already of the Array type. [See Here](https://gitlab.com/foundrynet/foundryvtt/issues/1155) for more details.
* The structure of Canvas Layer interaction listeners has been changed to delegate click and drag events from the base Canvas stage itself, rather than having each Canvas layer implement it's own interaction managers.
* Previously, updating a Compendium entry required importing the entity to the World, updating the Entity data, deleting the previous entry from the Compendium, and re-importing the updated version. This was a really awkward workflow, and can now be replaced with a much more elegant API method to edit compendium content directly. Please note that there is not yet a UI-based method for doing this in-game, but that functionality can be added in a subsequent update now that the underlying API exists. [See Here](https://gitlab.com/foundrynet/foundryvtt/issues/1066) for more details.
* A `Combat` entity will now persist the prior `(round, turn, tokenId)` which can be used to understand what has changed relative to the prior combat state.
* Improved the behavior of the `Entity.create` method to accept dot-string style properties provided as part of the initial creation request.
* The `ContextMenu` event handler now allows events to propagate even if a context menu is triggered, in case other systems or modules are awaiting a right-click event for other reasons. Furthermore, the triggering event which spawns a ContextMenu UI can now be configured as an additional option when the menu is instantiated.
* The initial implementation of localization support erroneously named the localization module as `il8n` when it should be `i18n`. This has been renamed.
* The CSS rules for Applications has been overhauled to make extensive use of `overflow-y: auto` instead of `overflow-y: scroll`. This could cause some styling changes to be forced upon downstream modules.
* Switched the Scene Notes application to activate it's editor via a button instead of starting with the editor always active.
* The set of active `Application` instances which should be refreshed when an Entity data is updated has been converted from an Array to an Object. This is still recorded as `entity.apps`, but this is now an object where the keys are appIds and the values are Application instances.
* Deleting a `Scene` entity will now propagate deletion to `CombatEncounter` and `FogExploration` documents which belong to that particular Scene.
* Added global constants for the allowed file extension types allowed for different media as `IMAGE_FILE_EXTENSIONS`, `VIDEO_FILE_EXTENSIONS`, and `AUDIO_FILE_EXTENSIONS`.
* The FilePicker ui will now dispatch an `onChange` event to the linked input field when a file is selected in the picker.
* Standardized the `user-select` styling rules across browsers including Firefox, Opera, and Safari.
* Applied a sensible tabulation order to the Playlist Track configuration sheet.
* Fixed the behavior of the `JournalEntry.show()` method to correctly force display of the Journal content if (and only if) the force parameter is passed as true.
* Added support for `flags` in the data model for Folder entities. Folder flags can be used by modules or systems to store certain data at the Folder level which modifies behavior of that folder (or its contents).
* Changed the behavior of the `Roll.parts` Array to now be immutable. Once rolled, the `roll` method cannot be called again, however a `reroll` method has been added which provides a Factory for creating a new Roll object with the same formula and data.

### D&D5e System Improvements

* Incorporate updates to the Class Features compendium using new pre-configured items provided courtesy of Thor's Wrath on Discord.
* Fixed a bug with experience gain per challenge rating for high CRs (26-30) which were previously incorrect.
* Redesigned the HTML structure of the D&D5e Actor Sheet to provide a more consistent and responsive experience across different browsers.

## Beta Version 0.3.2, 2019-06-28

Greetings friends, I am very excited to post the next Foundry Virtual Tabletop beta update, this time it's version `0.3.2` which adds a ton of amazing new features for both the core platform and for Dungeons & Dragons 5th Edition. This update includes improvements to Token Configuration, built-in Module Updates, better organization tools like Folder Colors and new Compendium types, as well as a litany of bug fixes and minor performance improvements. Additionally - this update features the first installment of a very exciting partnership and collaboration which I am thrilled to announce.

Foundry Virtual Tabletop is teaming up with *Stryxin from Forgotten Adventures* and *Penelope* (*Vyrnali*) to add high-quality compendium support for the SRD Monsters from the D&D universe. Stryxin is a fantastic artist who creates maps, tokens, assets, brushes, tiles and more. He is undertaking a grand project to draw and release (eventually) a token for every D&D5e compendium creature and - best of all - he has agreed to share those wonderful tokens with the Foundry VTT community free of charge. Penelope is a talented writer who is active in the World Anvil community who has graciously volunteered to author unique and flavorful bestiary entries for all monsters to give their biographies a special Foundry VTT touch which gives the Monsters compendium that extra ability to inspire you and your players. This FVTT update includes fully implemented game-ready tokens for all the CR0 monsters (29 of them)! Each entry has a customized biography, a beautiful drawn token, and fully configured stat blocks and abilities which are ready for use in-game. We will be continuing to collaborate to add tokens for higher CR enemies with each future update!

I'm really thrilled by the continued progress on this project and the inspiring modules being created by the community. Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

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

Greetings everyone, I am very excited to release the first incremental update from the `0.3.x` Beta generation of Foundry Virtual Tabletop. Thank you all so much for your continued testing and support. Without further ado, here is the `0.3.1` Beta update! This update contains 60 fixes and improvements following the massive `0.3.0` update from earlier this month.

As it is the first update following a new major version - update `0.3.1` is primarily focused on bug fixes and quality-of-life improvements which build upon the new major features. Despite that focus, there are several new key features which I hope that many of you will greatly enjoy. The most significant improvement in this update is a major performance improvement to *Fog of War* rendering which will allow Foundry VTT to scale to larger and more ambitious maps while maintaining the high level of performance which is a cornerstone of the project.

I'm really excited about the continued progress for this software and motivated by the support and encouragement of the community. Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

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

## Beta Version 0.3.0, 2019-05-29

Greetings friends, this release marks and exciting milestone for Foundry Virtual Tabletop as the software graduates to the `0.3.x` iteration of Beta development. There are several significant changes as part of `0.3.0`, so I hope you will carefully read these update notes. There are a lot of them this time - `0.3.0` is the biggest (in terms of amount of changes) update to Foundry VTT yet!

The key highlights of this new version include *Electron Migration*, improvements to the Walls system to support *many more wall options, including one-way and terrain types*, the new *Token HUD* which provides a better user experience in quickly editing token health or elevation values, the addition of *chat bubbles* which visually illustrate tokens in a Scene which are speaking in character, improvements to fog of war rendering performance (as much as a 50% reduction in GPU usage), and many smaller features and bug fixes. Overall this version addressed and resolved almost twice the number of issues of typical Foundry VTT updates. The size and scope of this update is substantial, so I would like to offer a sincere thanks to the testers who are helping me to evaluate it and identify any new bugs and feedback.

I'm really excited about the continued progress for this software and motivated by the support and encouragement of the community. Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### Please Read: Electron Migration

There is a key change as part of Foundry Virtual Tabletop 0.3.0 which deserves a section on its own to discuss. I have migrated the native application encapsulation from NWJS (https://nwjs.io/) to Electron (https://electronjs.org/) for a number of key reasons which I believe to make it the superior choice for ongoing development. The immediate consequence of this change is the following:

* There is no support to patch pre-existing versions of Foundry VTT to this new update version. Everyone must re-download the full application with the arrival of 0.3.0. Future updates will use the auto-updater feature, but this version requires a re-download.*

There are two primary advantages of Electron which motivated this decision. Application performance is measurably improved compared to the NWJS implementation. I hope users will find the Electron experience to be slightly more responsive. Secondly - using Electron supports an easier build process which will allow me to support native Linux and MacOS versions more easily in the future.

### New Features

* The native encapsulation layer for the application has been migrated to *Electron*. Please see the important paragraph above for more thorough explanation around the consequences and implications of this change.
* The Wall placeable object has been updated to support *many additional options for wall placement*. The previous appraoch of classifying walls using four prototypical types has been replaced with each wall object having granular control over how it affects movement, perception, direction of effect, and door configuration. The Wall placement tool now supports a greater number of prototypical options, but each wall may be manually configured by double clicking on one of its endpoints.
* The expansion of the walls system now allows for *one-way walls* which can restrict movement or perception from just a single direction while allowing it from the other. To make a Wall one-way only, go into the wall segment configuration and set the Direction property of the wall. The available directions "Left" and "Right" are denoted with respect to the direction of the wall ray. For example, if a wall is drawn from point A towards point B, along that ray "LEFT" would be to the left of B and "RIGHT" would be to the right of B.
* The expansion of the Walls system also supports a new type of perception rescriction - called "SECONDARY" in the wall configuration. This type of perception restriction allows for *Terrain Walls* which do not block visibility of the first collision, but do block visibility for subsequent wall collisions. Terrain type walls have a variety of awesome use cases and can add a lot of flexibility to the type of visual experience which can be created in Scenes.
* Added a *"Clone Tool" for wall placement* which will place more of the same type of wall which was previously placed or edited. For example, if you desire to use many segments of a specific wall configuration, you can follow a workflow where you configure just one segment of the exact wall type you want and then use the Clone Tool to place many more segments of that same type.
* Added new Wall placement tools for Terrain and Etheral wall types to quickly place prototypical versions of walls with those movement or perception restrictions.
* Added a new *Token HUD* which is activated by clicking and holding on a Token for a brief period of time. The HUD will allow you to quickly and conveniently edit the value of that token's attribute bars, update their displayed elevation property, and quickly access the configuration sheet for that particular Token. Only one Token can be focused with the HUD at a time, which will fade out when it is not immediately in use to retain an unobtrusive UI.
* *Chat Bubbles* have been added to show in-character messages spoken by particular Tokens. A message which is sent using either the /ic or the /emote prefix will be displayed from the perspective of the speaking Token as a chat bubble positioned above their token on the Scene HUD layer. Chat bubbles provide a nice way to immersively illustrate conversations or emotes occuring between characters in the world. This functionality may not appeal to all groups, so it is possible to disable Chat Bubbles as a world-level configuration option in the game settings menu.
* Added a new option to the Scene context menu to *Duplicate Scene*, creating a copy of the scene and all the objects it contains which can form the starting point for modifications to an existing map.
* The visual appearance of camera panning behaviors has been improved. These occur when TAB cycling between tokens, or when dragging your cursor to the edge of the screen during a Wall placement workflow. In such cases the canvas will now pan more smoothly for a nicer user experience.
* A previous update added the possibility of image type Journal Entries. While this was a nice addition, it put users in a position where a Journal Entry could only be an image OR a text entry. With this update, the multiple types of Journal Entries have once again been consolidated and each journal entry may have both image and text components. Buttons in the header of a Journal Entry allow you to toggle between the different modes.
* The functionality to handout a Journal Entry to players has been moved from the right click context menu of the Journal sidebar to the header of a specific entry which you want to hand out. This has several advantages - foresmost being that it allows for additional context of the share request to be implied. If the GM is viewing the text portion of a journal entry when clicking the "handout" button, players will also be shown the text component. If a GM is viewing the image component of a Journal Entry when it is handed out, the players will be shown the Journal Entry image.
* The title of Journal Entries has been suppressed for players whom do not have at least LIMITED permission to view the entry. This avoids spoiling the title of a journal entry to players when handing it out to show it to everyone (including those who lack normal permission).
* Added a new tool to *showcase Actor Artwork* or Token Artwork available in the right-click context menu for Actors and Items. This will display a pop-out UI which showcases the artwork in a more zoomed-in format. Moreover, this showcase can be handed out like a Journal Entry to show a profile image, token image, or item image to all connected players.
* Improved the display rendering of Scene-type Compendium packs.
* Substantially improved the performance of moving or deleting multiple Tokens at once using a group-selection workflow. These changes have been rolled out initially for Tokens alone, but the improvements will be generalized to benefit other types of Placeable Objects in a subsequent update.
* Added support to run Foundry Virtual Tabletop using `HTTPS and a SSL Certificate`. In order to run FVTT in SSL mode, you (for now, this process can be improved in the future) need to edit the `options.json` file to add two new attributes directing the application towards a SSL key certificate files for your domain. If these properties have been defined and point towards valid files, the server will automatically run using HTTPS instead of simply HTTP. See the following for an example: https://gitlab.com/foundrynet/foundryvtt/issues/466

### Core Bug Fixes

* Improve the user experience around chain placement of Wall segments. The system will now record the exact coordinate positions of a prior endpoint to ensure that no gaps are present. Furthermore, the wall placement workflow now incorpoates a rapid double-click detection filter which can prevent the accidental placement of very short walls in quick succession.
* Fix a bug for Ruler measurement - if a measured movement path experience a wall collision, it caused the Ruler to become in a somewhat broken state which prevented further measurement. Now if a movement is blocked by collision, you may continue measuring to find a valid path.
* Corrected a bug with editing placed Wall segments - in a previous version of FVTT collapsing a wall by dragging it's endpoints together would delete the segment. This behavior had gotten broken and was leaving stray walls around with identical endpoints. This behavior has been corrected and collapsing a wall segment will now delete the wall.
* Closed a loophole which allowed players to move a Token using a Ruler measurement workflow even if the game was currently paused.
* When a game system only has one Actor type, a bug was occuring when creating new Actors that would pop the only value out of an Array, making subsequent requests cause a breaking error.
* When placing or deleting a Token from a Scene which has vision or light emission settings, the current state of vision and fog of war was not immediately updating until that newly placed Token was updated by moving it. This has been addressed and the lighting/vision implications of placed or deleted Tokens should be realized immediately for all clients.
* Wall endpoint coordinates were not always correctly coerced to integer pixel coordinates. This has been addressed and all Wall endpoints are rounded to the nearest pixel before being saved to the database. This helps reduce data size and also avoids issues with tiny gaps between wall segments due to floating point precision issues.
* Some server-side validators were not correctly being applied. For example - it was possible to create an Ambient Sound object with no sound file specified as its audio path. This should have been prevented as a validation failure on the server side but was not. The application of data model validations has been improved to ensure that all objects are validated before they are saved to the DB.
* An Item sheet for an Owned Item would remain displayed even if that item was deleted from its parent Actor. Now, any sheets associated with an Owned Item will be closed automatically if that item is deleted. Additionally, Owned Item sheets were not previously uniquely IDed, which resulted in multiple sheets being opened for the same item. Now each OwnedItem is referenced in the ID strategy for the sheet, resulting in only a singleton DOM element per Owned Item.
* Alterations to Folder entities were not always immediately synchronized across all connected clients. This fix will allow Folder naming or permission changes to more reliably propagate as soon as they occur.
* It was possible for some functions which used the same event Hook to not get called in some situations when a previously called hooked function returned a "falsey" value instead of explicitly `false`. This has been addressed and all Hooked functions will execute as expected.
* Fixed a UI rendering bug with the PlayerConfiguration app which prevented the impersonated Character from being correctly highlighted for selection.

### Core Software, APIs, and Module Development

* Server side logging files are now produced. When running the application either using Electron or via Node.js, the `debug.txt` and `error.txt` files will be produced in the root Foundry directory. These files will contain valuable debugging information or errors which can help me better solve any issues which players encounter while using the software.
* An optional data object may now be passed to the `Application.render()` function which can allow Applications to conditionally tailor their rendering strategy to the components of a data model which were modified, triggering the render request. For example, Entities will now pass the updated (differenced) data to the render function when re-rendering active sheets.
* Each `PlaceableObject` subclass (Token, AmbientLight, MeasuredTemplate, etc...) now retains a reference to the Scene within which it resides. This makes identifying the parent container for an object more convenient as you may simply reference `object.scene`.
* Each `Application` class may now choose to define it's CSS `id` as a dynamic property as an alternative to a static option.
* Added the new `CanvasAnimation` helper class with methods which automate the process of linear (for now) animation of a canvas object between two values.
* Added a Canvas HUD layer providing the ability to render DOM elements with a positioning relative to a canvas coordinate and scale.
* Performance of the fog of war rendering algorithm has been improved substantially! I identified a simplification which resulted in fewer containers needing to be drawn to the canvas which, in my own testing, reduced GPU utilization between 30 and 60% for most Scenes.
* The `alias {String}` attribute of the ChatMessage entity data model has been deprecated in favor of a `speaker {Object.{actor, scene, token, alias}}` attribute which captures more (optional) data about the origination of a particular chat message or dice roll.
* The ChatMessage data model has been extended to explicitly track the `emote {Boolean}` property to record whether or not a message is of the "emote" type - allowing modules and systems to customize the rendering of emote messages differently from others.
* Improve upon the way that Application instances are rendered and positioned. This allows for more flexible configuration of application scale and position which can be specified either using CSS or using JS at render time.
* The `Canvas.dropActor()` method has been moved to `TokenLayer.dropActor()` and it's signature has been improved to offer some additional customization options for how the Actor data is translated into a newly placed Token.
* Much of the client-side socket behavior has been factored out and standardized within the `SocketInterface` helper class which is re-used throughout the client-side codebase. This guarantees a more standardized data contract and handling logic to ensure that various APIs which transact data with the server for saving adhere to the same conventions and prototypical method signatures.
* Previously, Module manifest `module.json` files were required to specify the `styles`, `packs`, and `scripts` attributes by passing empty Arrays if no assets of that type were included by the Module. Now these attributes may be safely omitted if none are included.
* Extended the signature of the `Entity.hasPerm()` method to provide an additional argument for whether to require an exact match or an inequality-based permission match.
* Modules may now request a specialized messaging socket be provided for their own use in exchanging data. Please see the following for more detail: https://gitlab.com/foundrynet/foundryvtt/issues/582
* An extensive backend standardization and compatibility pass has occured for the server side Document, EmbeddedDocument, Entity, and EmbeddedEntity data classes. This has improved and standardized the data management approach used by the server-side code.
* The server side code has been significantly overhauled and polished to feature better practices and more standardization for key server-side modules.
* Added an extra sanity check on server start to check for and protect against missing write permissions in the public directory of the application location.

### D&D5e System Improvements

* The display of all types of Item sheets has gotten an update - adding a consistently themed sidebar for all items which displays helpful summary information at a glance.
* Improve the tab navigation behavior of Item sheets - previously item sheets were resetting to the Description tab whenever a change was made - now the currently viewed tab will be correctly remembered and retained.
* Corrected several data errors in the Spells SRD.
