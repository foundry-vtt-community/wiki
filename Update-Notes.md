<!--tl=2-->
<!--ts-->
   * [Beta Version 0.4.X](#beta-version-04x)
      * [Beta Version 0.4.7, 2020-02-09](#beta-version-047-2020-02-09)
      * [Beta Version 0.4.6, 2020-02-04](#beta-version-046-2020-02-04)
      * [Beta Version 0.4.5, 2020-01-17](#beta-version-045-2020-01-17)
      * [Beta Version 0.4.4, 2020-01-09](#beta-version-044-2020-01-09)
      * [Beta Version 0.4.3, 2019-12-15](#beta-version-043-2019-12-15)
      * [Beta Version 0.4.2, 2019-12-10](#beta-version-042-2019-12-10)
      * [Beta Version 0.4.1, 2019-11-20](#beta-version-041-2019-11-20)
      * [Beta Version 0.4.0, 2019-11-15](#beta-version-040-2019-11-15)
   * [Beta Version 0.3.X](#beta-version-03x)
      * [Beta Version 0.3.9, 2019-10-21](#beta-version-039-2019-10-21)
      * [Beta Version 0.3.8, 2019-10-05](#beta-version-038-2019-10-05)
      * [Beta Version 0.3.7, 2019-09-14](#beta-version-037-2019-09-14)
      * [Beta Version 0.3.6, 2019-09-10](#beta-version-036-2019-09-10)
      * [Beta Version 0.3.5, 2019-08-20](#beta-version-035-2019-08-20)
      * [Beta Version 0.3.4, 2019-07-31](#beta-version-034-2019-07-31)
      * [Beta Version 0.3.3, 2019-07-17](#beta-version-033-2019-07-17)
      * [Beta Version 0.3.2, 2019-06-28](#beta-version-032-2019-06-28)
      * [Beta Version 0.3.1, 2019-06-16](#beta-version-031-2019-06-16)
      * [Beta Version 0.3.0, 2019-05-29](#beta-version-030-2019-05-29)
<!--te-->

# Beta Version 0.4.X

## Beta Version 0.4.7, 2020-02-09

Greetings friends, adventurers, and supporters. I am excited to share the Foundry Virtual Tabletop Beta 0.4.7 Update which is a stable update version released for all Patreon supporter tiers.

This update extends the 0.4.6 update to add improvements for Dice rolling with support for new nested expressions and dice pools, improvements to Token interaction, UI optimizations, and API improvements. This update improves upon these major features with a number of bug fixes and performance improvements. Please visit the following URL to review the update notes from the prior 0.4.6 update: [http://foundryvtt.com/notes/notes-0.4.6.html](http://foundryvtt.com/notes/notes-0.4.6.html).

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the [Foundry VTT Issue Tracker](https://gitlab.com/foundrynet/foundryvtt/boards) for visibility into development progress and which features are coming up next!

### New Features

- The End User License Agreement (EULA) has been updated with some language changes. The alterations include clarification around the terms of use about where the software may be installed, what steps must be taken if the license is refused, clarification around ownership of personal data, a change to the policy about what data is collected (none, except when the software is updated), and some other minor adjustments. As a result of the EULA changes you must review and accept the updated agreement after installing this update.

### Core Bug Fixes

- Corrected issues with sorting Entities and Folders in the sidebar which resulted from changes in the application rendering callback logic.
- Fixed issues with dice rolls and parenthetical expressions which prevented some Math operations like floor, ceil, or round from being parsed correctly.
- The new Dice Pool construct was incorrectly keeping only the highest result from the pool when constructed using the fromFormula() factory method. Now Dice Pools will sum any surviving results in the pool after dropping or modifying individual rolls.
- Fixed three issues related to a custom configured route prefix: the [socket.io](socket.io) connection path was not served with respect to the prefix, the uploading of files to the server-side file storage used the incorrect POST destination, and image files selected through the FilePicker incorrectly left the route prefix path in their saved paths.
- Handled an edge case with the changes to the KeyboardManager where the enter key on the numpad was treated as a different keystroke than a regular Enter keypress.
- Fix an incorrect typing of the Application.rendered getter which was returning an integer instead of a boolean. This fix corrected a few downstream issues including Journal Entry sheets which did not render images properly.
- Correct two errors in the CONFIG object which caused the Macros Directory to be undefined and for the FolderConfig sheet to be incorrectly assigned.
- When a World has no active scenes, creating a first scene will automatically activate it - but other connected players were not automatically pulled to that new scene as you would expect.

### Core Software, APIs, and Module Development

- Added a hook for all Application subclasses which fires when that application is closed. See the following GitLab issue for example usage: [https://gitlab.com/foundrynet/foundryvtt/issues/2100](https://gitlab.com/foundrynet/foundryvtt/issues/2100)
- Added the `Roll.cleanFormula(formula)` method for standardizing the string format of a dice roll formula, removing redundant spacing or arithmetic operators.
- Allow combatants which do not have a Token reference to remain under GM ownership.
- Improve the flexibility of the Entity.hasPerm() method to work for entities which do not contain an explicit permissions object (like Folders).
- Specifying a gridDistance in a game system manifest is no longer strictly required, but simply optional.
- Correct uses of the PIXI Graphics beginTextureFill method to adhere to the new recommended object-based signature.

## Beta Version 0.4.6, 2020-02-04

Greetings Patreon supporters and Beta testing community - and welcome to the release notes for Foundry Virtual Tabletop Beta 0.4.6. This is an "unstable" (even-numbered) release which adds many new features, API changes, and underlying software improvements. These changes are released to Council tier testers for preliminary testing and will be included in the Beta 0.4.7 stable release coming next week for all Beta tiers.

This update focuses upon improvements for Dice rolling with support for new nested expressions and dice pools, improvements to Token interaction, UI optimizations, and lots of API updates.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- Added support for Nested Expressions and Dice Pools in Dice rolling expressions and in the API. A "nested expression" allows for evaluating an inner variable or roll as part of an outer roll expression, an example of what this empowers is for the number of dice which are rolled to be variable like `(@details.level)d6` or `(1d4)d8`. A Dice Pool allows for combining multiple Roll expressions into a set and computing the total for the set after modifying or dropping certain outcomes, for example `{3d8,4d6}kh` or `{2d8,3d6,4d4}cs>=7`. To learn more about how nested expressions and dice pools work please review the updated Dice Rolling documentation page: [http://foundryvtt.com/pages/dice.html](http://foundryvtt.com/pages/dice.html)
- The concept of "Scene Notes" has been retired as an element of the Scene data model directly. Instead now all Scenes have a journal attribute which can reference an existing Journal Entry which provides the notes for this Scene. Any Scene which previously had scene notes defined will experience a migration when the World is first loaded into 0.4.6 which will create a corresponding Journal Entry using the contents of the Scene Notes and automatically link that created Journal Entry with the Scene. To share a bit of historical context - the Scene Notes concept was added before the Journal existed as a way to track GM and session notes about a particular scene. The functionality of the Journal provides a far more flexible way to write notes, however, so moving the old scene notes concept to use the Journal system is a nice consolidation which eliminates a redundancy and helps to simplify things.
- The visual scale of the Token HUD has been improved to scale dynamically based on the grid size of the Scene and the size of the Token itself. The layout for the Token HUD has been normalized to a 100px grid scale - but this improvement allows the same proportions and orientation of the HUD to scale effectively for smaller or larger grid sizes while keeping the user experience the same.
- Improved the positioning of Token nameplate text relative to the lower edge of the token frame by making the amount of vertical padding a function of the grid size used.
- Improved the visual appearance of Token attribute bars for large-sized tokens by limiting the vertical height of the bar where previously large Tokens (for example Huge+ creatures) would have unnecessarily large health bars.
- Keyboard based token rotation did not previously work with numpad keys - as SHIFT+numpad was incorrectly detected as some other key (like Page Up) instead of a modified numpad keypress. The refactoring of the KeyboardManager utility has allowed this functionality to be handled correctly.
- "Fast" token rotation (SHIFT+wheel) now snaps to 60 degree increments to hex grids to allow for tokens to rotate towards hex vertices. Fast rotation remains at 45 degree increments for square and gridless modes. Slow rotation occurs at 15 degree increments for all grid types.
- Changes to the set of modules which are active within a World will now force a hard refresh for all connected users, not just the GM user who changed the set of active modules.
- Improved the handling of user cookies to forcibly unset an existing cookie when a new authentication request is made.
- Improved the reliability of Fog of War persistence by implementing an event trigger which fires when the browser tab is being closed to perform a final fog of war save in the event that the user had additional fog changes that were not yet synchronized with the server.
- Redesigned the system which displays user activity and connectivity status to more reliably show which users are connected to the game session and viewing which Scene.
- Record which Tokens a user had targeted when the canvas is being re-drawn in order to ensure that the same tokens remain set as targets after canvas rendering is complete. Previously if the canvas was re-rendered (for example when resizing the browser window), the set of targeted tokens would be lost in the process.
- Redesign the process for chaining Wall creation and wall endpoint grid snapping to greatly improve the process and eliminate small gaps which could occur when rapidly chaining wall segments together.
- Core improvements to the application class make it easier to defined certain HTML containers which should remember their vertical scrolling position when the application is re-rendered. This new functionality is used to improve the behavior of lengthy Roll Tables which will now preserve their scrolling position when the table is re-rendered.
- Interface notification messages can now be prematurely cleared by clicking on them without needing to wait for them to disappear naturally.
- Added a tooltip for Macro buttons in the Hotbar UI which displays the name of the macro when hovering over the button.
- Add some missing tooltips and localization translations for Combat Tracker control buttons.

### Core Bug Fixes

- Fixed a performance issue from a GPU memory leak which occured when rapidly interacting with walls or door configurations due to stale fog of war rendered textures that were not destroyed.
- Limit the set of Actors which can be chosen when configuring a Token to only display those which the current User has ownership permission over.
- Fix a crash which could occur in the Combat Tracker when changing Scenes using a popped-out tracker display.
- Copy+paste operations for canvas objects like Tokens were not correctly using the MacOS Command key, instead requiring the Control key. These operations now use the CMD key as expected for Mac environments.
- Fixed an issue with changes to the items array for a synthetic Token Actor which failed to result in re-rendering of an open Item sheet. Now changes to the owned items for a synthetic Token actor will allow item sheets to automatically re-render as necessary.
- A Token which references an inaccessible image for it's artwork could not have it's visibility state toggled as the lack of a loaded texture caused a failure in toggling the visible state of the token.
- Fix incorrect handling of zero initiative values which were incorrectly sorted below negative values due to a mis-specified logical test.
- Editing multiple controlled wall segments was no longer working after the embedded entity ID changes in 0.4.4. This functionality has been restored.
- The visual position of door controls was not properly updating when wall positions or types were modified. Now when changes to a wall segment are processed the door control for that segment will be re-rendered.
- Choosing a macro image with the file picker caused the Macro edit sheet to close or to become locked for editing. This has been resolved.
- Fixed an issue with application of the default scene position which could force certain large maps from becoming permanently stuck "out of bounds" and unable to zoom.
- Corrected a bug where deleting the text of a drawing caused a (harmless) error in the console.
- Fixed a bug with canvas object undo operations which caused only every-other operation to be reverted due to dome duplication of array management.
- Corrected a failure in importing Journal Entries into a World from a compendium pack.
- Fix a bug where providing an explicit name attribute when creating a Compendium pack through the API produced a server-side error when a default name was inferred from the text label.
- When the application is launched with a `--world` startup option where that world cannot be launched because it does not exist or is out-of-date, the application will go to the Setup page instead of loading an invalid world state, displaying a log message to inform the user why their requested world has not loaded.
- Fix a layout issue with the Macro Hotbar which caused the context menu for Macro buttons to underlap the AV camera views.
- Fixed a layout issue with the Macro Hotbar which caused it to capture pointer events (mouse clicks) even when the bar was in a collapsed state.
- Correct a bug in the `RollTable.draw()` method which caused that function to fail if both the optional result and roll arguments were omitted.
- Solve a bug resulting from multiple sidebar tab render requests.
- Fix a bug for newly created Actors which prevented the name field of their prototype token from being immediately editable until the application was reloaded.
- Correct a regression with animated tokens which prevented them from working properly due to changes in the way that token source textures were loaded.
- Server side validation for various image fields was not configured to allow for inline base64 png or jpeg data which (in some cases) should be allowed.
- Fixed a permissions issue which prevented Users from being able to roll initiative for combatants that they have ownership rights for in the Combat Tracker.

### Core Software, APIs, and Module Development

- [BREAKING] Refactor the KeyboardManager class to stop using the deprecated event.keyCode property and move towards more modern string-based codes which define which keyboard keys are preseed. If you currently use the Keyboard Manager (or its instance `game.keyboard`) you may be impacted by this change.
- [BREAKING] Move the position of the `canvasInit` hook event to occur before canvas layers are rendered rather than afterwards. This is more conceptually consistent with an "initialization" hook in that it allows modules and systems to modify data or configuration before rendering work occurs.
- [BREAKING] Please note - the elimination of Scene Notes only affects Scenes which were within a World. If you have modules or systems which provide Scene compendium packs those scenes will not automatically have journal entries created for their Scene notes. You will need to create a companion Journal Entry compendium pack with entries for your Scene notes to be distributed as part of your module. The scene notes can still be accessed under `scene.data.description` and will remain until at least version 0.5.x in order to allow time for migration.
- [BREAKING] Form fields which specify a numeric data type will have their input value automatically converted to `null` if the input field is submitted as an empty string. Previously these empty strings would be converted to zero which could lead to potentially undesirable results.
- [BREAKING] Removed the `entryTime` attribute from the data model for a Journal Entry as this field was not used by any system in the core software.
- [BREAKING] Some changes in previous versions to server-side validation methods resulted in timestamps that were stored in an ISO string format instead of as a numeric seconds since UNIX epoch. This has been standardized and all timestamp type fields will be stored as a numeric data type consistent with the return value from `Date.now()`.
- [BREAKING] Refactored and converted the default behavior of Form Applications which previously supported a `submitOnUnfocus` option that would automatically submit the form when a form field fired the unfocus event to instead use a new option `submitOnChange` which fires whenever the change event occurs. The end user experience is very similar, as unfocus events will trigger the change event if the field contents were altered - but this has the added advantage of allowing the user to press the enter key to confirm a pending change and submit the form.
- Comprehensively refactor the `CONFIG` object to move its definition to the very end of the client-side script, allowing for direct references to classes and objects to be used with CONFIG is defined rather then scattered throughout the codebase. Remove or re-work any references to CONFIG variables to ensure they are deferred until after the CONFIG object is declared.
- Implemented a global `uuid` attribute for all Entities and Embedded Entities which provides a canonical reference to any piece of data. This functionality will be used more prevalently in the future - but for now you can take advantage of the `uuid` attribute on Entities, PlaceableObject instances, and Compendium entries as well as the `fromUUID(uuid)` method which can construct an appropriate object from any universal identifier string.
- Expose the `Actor.modifyAttributeBar()` method which is responsible for updating Actor data when a Token bar is changed. This allows game systems or modules to change how alterations to a Token resource should be applied to the Actor data model - for example accounting for temporary hit points in the D&D5E system.
- Move the `active` and `scene` fields out of the User data model and re-define them as transient activity data that is only persisted in memory during the session as part of user activity tracking. These fields of the User data model have been removed and replace with properties on the User entity which can be used in a similar way.
- Add configuration references to all of the primary UI elements used throughout the default interface in `CONFIG.ui`. This has the joint benefit of organizing and centralizing the definition of what classes are used for what element as well as allowing for the possibility for modules and systems to override this configuration and provide an alternative application to be used instead of a default UI element.
- Refactor the `SidebarTab` abstract application to remove the requirement that a specific tab name be passed into the constructor which helps to standardize the initialization signature.
- Implement the `Die.fromFormula(formula)`; factory method which can construct a Die instance from a given string formula using the dice rolling syntax.
- Implement the `DicePool` class which accepts an Array of `Roll` instances as well as a modifier query string and resolves the set of Rolls within the pool.
- Implement the `DicePool.fromFormula(formula);` factory method which constructs a DicePool instance from a given string formula using the dice rolling syntax.
- Migrate the handling of die roll modifiers from the Roll class into the Die class which is a more logical place to maintain these modifications to an existing Die instance.
- Added support for radio-style form field inputs in form application processing. This allows for multiple input fields to have the same name attribute. In such cases all values from these inputs are concatenated into an array which is passed onwards for form submission and handling.
- Impose 9999 as a maximum zIndex which application windows can assume to ensure that module developers can define a UI layer starting from a zIndex of 10000 which is guaranteed to be drawn above any pop out application window.
- Application subclasses can now easily define HTML containers that should remember their vertical scrolling position when they are (re)rendered. To use this feature, add the `scrollY` property to the defaultOptions object for the application class. See the `RollTableConfig` class definition for an example usage.
- Refactored a large number of usages for canvas object manipulation methods which no longer need to pass sceneId as their first parameter.
- Added entries in the `CONST` object which enumerate the supported roll types.
- Added a new hook for chat bubble rendering which allows hooked functions to modify the content of resulting chat bubble HTML. See the following issue for an example: [https://gitlab.com/foundrynet/foundryvtt/issues/1942](https://gitlab.com/foundrynet/foundryvtt/issues/1942)
- Improve the behavior of the Compendium.getEntity() method to return null if the requested entry ID does not exist in the pack.

### Documentation Improvements

- Updated dice rolling documentation page: [http://foundryvtt.com/pages/dice.html](http://foundryvtt.com/pages/dice.html)
- Updated API docs built for the latest 0.4.6 codebase. [http://foundryvtt.com/api/](http://foundryvtt.com/api/)

### Known Issues

- If non-GM users are connected to the session when the first Scene is created, they are not automatically transitioned to that scene when it is activated.
- In some cases, World-level compendium packs which share the same pack name in multiple worlds can get cross-contaminated when a world is closed and another world is opened without restarting the VTT application.
- Changes to the permissions object of Entity data does not immediately update the editable state of some rendered applications.
- Some issues currently exist with using an optional route prefix for running the FVTT application. You may wish to consider removing a route prefix for now until this feature is further stabilizied in the 0.4.7 update.

## Beta Version 0.4.5, 2020-01-17

Greetings Patreon supporters and Beta testing community - I'm happy to release a the stable version update for Foundry Virtual Tabletop - Beta 0.4.5. This is an "odd-numbered" release, which means it implements bug fixes and stability improvements for all the new features that were added in Beta 0.4.4. If you haven't yet gotten a chance to take a look at the release notes for that update, please do check them out: [https://www.patreon.com/posts/33025153](https://www.patreon.com/posts/33025153)

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- Bypassing snap-to-grid by holding SHIFT while placing Walls has been (temporarily) disabled. This feature was contributing to the addition of small gaps between walls where endpoints did not perfectly align. I will be redesigning the wall snapping and chaining system in 0.4.6 to re-enable this feature with improved behavior.
- Creating a Macro by clicking on an empty Hotbar slot will now automatically populate that slot with the created Macro.
- Minor improvements to the HTML structure and layout for Combat Tracker encounter and round controls.
- Minor improvement to the visible shading of Scene titles to better stand out against light backgrounds.
- Minor styling improvement to the list of Actors selected in a Player Configuration sheet.
- Add a new automatic migration for Scene entities which occurs when the System data version is incremented to ensure that Token actor override items are properly migrated.

### Core Bug Fixes

- Worlds could become broken in a state where each time the world was launched the server would attempt to create a new Gamemaster user, which would fail due to that user name already being taken. If you find yourself impacted by this issue, perform the following steps to correct the problem: [https://gitlab.com/foundrynet/foundryvtt/issues/1955](https://gitlab.com/foundrynet/foundryvtt/issues/1955)
- The id of an Item entity was inadvertently locally deleted when using it in a drag-and-drop operation on an Actor sheet.
- Fixed a problem where sidebar Entities could no longer be sorted into a new Folder because of breaking changes in the 0.4.4 relative sorting method.
- Popped out sidebar tabs failed to automatically resize when their contents were re-rendered.
- Fix an issue with Token creation which casued it to be drawn twice - resulting in an orphaned token image that would remain shown even as other aspects of the Token appearance were changed.
- The Table Result drawn from a Roll Table was incorrectly displayed publicly when drawing from the table using a Self Roll, now fixed as a private self-drawn result.
- Undoing a drag movement for a Tile or Drawing resulted in the object remaining locked after it's movement was reverted. This no longer occurs.
- Right clicking on an empty Hotbar slot no longer throws a console error.
- The data type of User.role was inadvertently changed to a string when submitting the Player Management form.
- The speaker object for Chat Message data did not properly contain the new style Token ID. As a consequence some aspects of chat messages that relate to Tokens (like Chat Bubbles) did not function properly.
- After closing a minimized sheet, it would become impossible to minimize the sheet again once re-opened.
- Fixed a bug with the on-update workflow for Journal Entry changes to properly update the status of Map Notes.
- Default Scene Playlist switching did not occur properly when using a Scene.updateMany operation.
- Fix a bug related to new server-side permission controls that prevented a Player from ending their own turn in Combat.
- Fix a bug related to new server-side permission controls that prevented a Player from opening or closing a door in a Wall object.
- Invalid compendium collection name in a dynamic entity link would result in a failure to convert the string into a link and also crash the sheet render.
- Ensure that Scene entities which are duplicated do not maintain an active, viewed, or shown in navigation bar status of the copy.
- The Round number and Ent Turn buttons in the Combat Tracker were not reliably displayed on the tracker.
- The toggle visibility and defeated state buttons in the Combat Tracker were not working properly due to the Token id changes in 0.4.4 which weren't handled correctly. These combatant controls are now working properly.
- Issues with Player Configuration avatar editing - causing infinite recursion.
- Modifying the text attributes of a Drawing failed to properly re-draw it's appearance. This has been corrected.
- Changes to a Token width or height attribute must trigger a complete re-draw of the token instead of just a minor refresh.

### Core Software, APIs, and Module Development

- Added a new `Entity.clone()` method to provide a standardized mechanism for an Entity to be copied in a way that results in a newly created Entity.
- The ChatMessage.createMany method now supports passing a Roll instance to each entry in the data array.
- Eliminate an unnecessary re-render operation for Journal Entry sheets when switching between Image and Text modes.
- The command attribute of a Macro entity is now allowed to be an empty string, where previously a non-empty string was required.
- Improve handling of the default Scene position to allow it to be null and to avoid accidentally replacing it with a non-null object in cases the initial position is not used.
- [BREAKING] Change the entity option of the ImagePopout class to avoid including an actual Entity instance which results in circular JSON serialization. Instead just include Entity metadata.
- [BREAKING] Remove the unnecessary and unused (by the core software) Entity.owner setter method.
- Correct the behavior of the Folder.parent getter to properly return a Folder entity (or null).

## Beta Version 0.4.4, 2020-01-09

Hey there everyone, I'm thrilled to present Foundry Virtual Tabletop - Beta 0.4.4 - the biggest Foundry VTT update ever released. An absolute mountain of work has gone into this update and it delivers an impressive list of really meaty features including the first version of the Macro System, expanded Scene options like default position and audio playlist, the ability to pull to Scene, and an enormous number of architectural and API improvements.
Please Note

Due to the substantial core changes to various aspects of the API - this update is somewhat more disruptive than normal. Modules and Systems have been automatically disabled until they can are updated for compatibility with 0.4.4. Furthermore - I do expect there to be some latent bugs related to the Macro system and the overhauled embedded entity management which could cause some friction. Please do not update to 0.4.4 immediately if you are a bit risk averse, however please do update if you are willing to help test these changes and ensure they are working properly.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- **Macro System. Added the first version of the Macro system to Foundry VTT. Macros allow for user**s to quickly activate chat or script based commands. Please note, this is just V1 of the Macro system which will continue to receive investment in future updates, so expect more Macro features in the future and be please be patient with limitations of the initial implementation. All players have permission to use chat-based macros, but players must be given special permission to use script based macros in addition to having the TRUSTED permission level.
- **Macro Hotbar**. Added a Hotbar UI element at the bottom of the screen which contains Macros as interactive buttons. The hotbar supports 5 pages of global macros which can be dragged and dropped to organize as you wish. Left clicking a Macro button triggers its effect. Right clicking the button displays a context menu of Macro options. The number keys 1 through 0 activate numbered hotbar slots and pressing the delete key while hovering over a Macro will remove it from the bar.
- The Electron application will no longer start automatically in fullscreen mode, but rather as a maximized window. This can be configured in the options.json configuration file.
- Overall aesthetic styling for Application windows has been refreshed with a more subtle parchment texture and color scheme.
- Scenes can now be configured to have a "Secret Name" which is shown to players in the navigation bar instead of the actual Scene name. This can help in cases where the Scene name could constitute a spoiler or is too lengthy.
- Added a new feature which allows a Gamemaster to pull a User to their currently viewed Scene. This option is available in the User context menu. Right click on a specific User and click "Pull to Scene" to cause that user to transition their canvas view to your currently viewed Scene.
- Scenes can now be assigned a Default View position which customizes the initial camera position when first viewing the Scene. Note that players who own a Token in the Scene will always start with the view centered on their Token location regardless of the default view position. To easily set the default view, open the Scene configuration sheet and zoom the canvas to your ideal position, and click the helper button on the sheet to capture the current camera position.
- Added support for a default Audio Playlist for each Scene. The Scene Playlist will automatically begin playing when the Scene is activated while the Playlist for the previously active Scene will stop (unless they are the same).
- Token images can now be mirrored horizontally as an additional checkbox option in the Token Configuration sheet.
- Added support to set the value for an attribute bar in the Token HUD to a negative number by explicitly prefixing the assigned value with an equal sign, for example =-10 would set the bar value to negative 10.
- Improved rendering performance for Drawing objects to make refresh operations after the initial graphic creation more efficient.
- Improve the fallback font used for Signika to allow a sans-serif font face that can better handle international character codes.
- Overhaul the functionality of the Combat Tracker to perform multi-update operations instead of serial database operations which greatly improve efficiency in cases where many Tokens are added, removed, or rolled simultaneously.
- Improve the automatic scroll position of the Combat Tracker when the turn order changes to keep the current combatant centered in the tracker view.
- Improve the permission handling for Measured Templates by adding a user field to the template schema and cross referencing the current user against the template creator to determine whether a user is able to make a change.
- Improve the permission handling for Drawing objects by cross-referencing the requesting user against the drawing author to better determine whether update or deletion operations can be allowed.
- Refactor the Folder entity to change the way that deletion workflow occurs, improving the reliability of cascading deletion or re-mapping contained entities or subfolders to a new parent.
- Improved server-side permission checking for Chat Message updates to allow users to make edits to their own created messages.
- The animation speed for Roll Table draws has been improved to perform better for very large tables with many entries. The total animation speed is capped at 2 seconds where previously rolling could take several seconds for very large tables.
- The visual display of the Alternate Token Image selection box for Tokens with a wildcard image is now more readable by trimming the common directory path and only showing the alternate filenames.
- Improved Entity sorting in the sidebar to automatically process any unsaved changes on an open sheet before moving the entity or assigning a new sort order.
- Automatically switch to the relevant Sidebar Tab when importing an Entity from a compendium pack.
- Provide a new configurable world-level option to choose between flat-topped and rounded cone template types as different cone template rules may be preferred by different groups or by different game systems.

### Core Bug Fixes

- Clicking the "Return to Setup" button on the Update Notes ui will now close the window as intended. I apologize to everyone who loved this bug and had hoped I would keep it forever.
- Fixed a serious bug where multi-token update operations were incorrectly applied in the active Scene, even if that scene was not the correct parent Entity requested in the operation.
- An issue which could cause a Folder to become self-referenced as its own parent was not correctly fixed in the last update allowing this issue to resurface. The server-side validator which prevents this has been re-written to (hopefully) solve this issue permanently.
- Avoid adding "undo" canvas operations to the history array which sometimes resulted in infinite undo recursion.
- Fixed an issue with the delete button on the Combat Tracker which caused it to remain disabled even if the confirmation dialog was declined.
- Corrected a problem with the Token HUD which prevented the bar control from being displayed in cases where the bar value was zero.
- Using the `mergeObject` utility function to unset an inner object property in cases where the parent object does not exist resulted in inserting an erroneous key into the original object. See [https://gitlab.com/foundrynet/foundryvtt/issues/1907](https://gitlab.com/foundrynet/foundryvtt/issues/1907) for details.
- Fixed tooltip wording on the Join Game screen.
- The configured route prefix operation for the Express server was not working as expected due to a number of relative links which were incorrect in the presence of a route prefix. These links have been updated to always include the prefix (if one is set) and this server configuration option should now work as expected.
- A typo in the server-side socket registration prevented system-level dedicated socket channels from working properly. After the change, assigning `"socket": true` in your system manifest will correctly enable you to use the `"system.{systemName}"` messaging socket.
- Fixed a problem with initiative calculation for the Combat Tracker which was not correctly using the synthetic Token Actor and instead using the base Actor for Tokens which were unlinked.
- Correct a problem with Compendium directory scroll position not being preserved after a re-render operation.
- Resolved a problem for Journal Entries where the image for an entry could not be changed in cases where the existing image assignment pointed to an image file that did not exist or was unavailable.
- Solved a Journal Entry bug which could prevent entries which had Limited permissions assigned from opening for a Gamemaster user.
- Fixed a bug with Roll Tables which caused a table formula which matched no available results to cause the table to become un-rollable.
- Roll Table entities viewed from a Compendium pack will now correctly have the Import button in their sheet header. Additionally, the header Import button had issues for other entity types which has also been fixed.
- Several buttons on a Roll Table sheet were hoverable for users who do not have ownership permission over the table, creating the false impression that operations were possible. Specifically the balance, lock, and delete entry icons are no longer shown as interactable to non-owners.
- Non-Gamemaster owners of a Roll Table were unable to create new result entries within the table. This has been corrected and Users can now be given permission rights to create table results if they have ownership of the parent table.
- Users who had observer (but not owner) rights to a Roll Table were not able to roll the table. This has been changed so Users can be given permission to roll a table but not to edit it.
- Fixed two problems which occurred when changing the primary result type of a Roll Table result.
- Improved a visual bug in the error message when entering the incorrect access key on the join page.
- Improved the copy+paste workflow for Placeable Objects to maintain the visibility state when pasting. For example, hidden Tokens which are copied will be pasted as hidden.
- Fixed an edge case bug where importing Scene data from JSON while actively controlling a Token or other placeable caused an exception, causing the import to fail.
- Fixed a bug which prevented it from being possible to remove a tiling texture from a Measured Template or Drawing without needing to refresh the application for the change to become visible.
- Corrected a problem where Measured Templates could become unselectable if saving an invalid texture path.
- Fixed a problem which prevented Journal Entries from being dragged into text fields to become dynamic entity links.
- Corrected an issue for A/V server configuration in cases where the connecting user does not have any access key assigned.

### Core Software, APIs, and Module Development

- The required core compatibility version for modules and systems has been set to `0.4.4` due to the large number of breaking changes included in this update. All modules and systems must review the changes and update their package manifest files to support `minimumCoreVersion` of 0.4.4. I created an overview issue that provides some high-level explanation of the larger API changes in this update. If you are a module or system developer, please see the following issue: [https://gitlab.com/foundrynet/foundryvtt/issues/1919](https://gitlab.com/foundrynet/foundryvtt/issues/1919)
- Added a number of new API concepts related to the new Macro entity. See [http://foundryvtt.com/api/Macro.html](http://foundryvtt.com/api/Macro.html) and [http://foundryvtt.com/api/Hotbar.html](http://foundryvtt.com/api/Hotbar.html) for API details.
- Further standardize and simplify Socket Interface workflows to use the same preHook and postHook signatures for all CRUD events. See [http://foundryvtt.com/api/SocketInterface.html](http://foundryvtt.com/api/SocketInterface.html) for details.
- Add universal support for multi-target database operations for all Entity and Embedded Entity types. See [https://gitlab.com/foundrynet/foundryvtt/issues/1820](https://gitlab.com/foundrynet/foundryvtt/issues/1820) and [http://foundryvtt.com/api/Entity.html](http://foundryvtt.com/api/Entity.html) for more details.
- This update introduces a major refactor to the structure of Embedded Entities which are now indexed by a unique string `_id` instead of a numeric `id`. Furthermore, embedded entity management has been comprehensively redesigned to standardize with a set of methods on the Entity class. See [http://foundryvtt.com/api/Entity.html](http://foundryvtt.com/api/Entity.html) for details.
- Comprehensively refactor the server side Document, Entity, EmbeddedEntity abstractions in the database document model to standardize and simplify the code structure.
- The `Collection.index()` method has been removed as it was not used by any core application.
- Added support for an optional `strict` parameter in the `Collection.get` operation which will raise an exception if the requested Entity ID does not exist.
- Implement a new `filterObject` method which allows for socket update operations to broadcast back only the subset of valid keys and values which were successfully applied during the update.
- A mapping of all synthetic Token Actors is now easily available under `game.actors.tokens` which provides a synthetic `Actor` instance for every Token id.
- Added helper methods to the User entity to assist with macro management. See the following issue for details: [https://gitlab.com/foundrynet/foundryvtt/issues/1935](https://gitlab.com/foundrynet/foundryvtt/issues/1935)
- Added a hook allowing systems and modules to customize Hotbar drop behavior. See [https://gitlab.com/foundrynet/foundryvtt/issues/1941](https://gitlab.com/foundrynet/foundryvtt/issues/1941)
- Simplified the distinction between `draw()` and `refresh()` operations for all Placeable Object subclasses. Draw operations are more comprehensive, completely re-constructing the canvas object while refresh operations are more lightweight, updating it's display in-place.
- Redesigned the `filterObject()` utility method to work using 2 objects. See [https://gitlab.com/foundrynet/foundryvtt/issues/1918](https://gitlab.com/foundrynet/foundryvtt/issues/1918) for details.
- Improved the `Dialog.confirm()` wrapper to return a Promise which resolves once the prompted user makes a choice. See [https://gitlab.com/foundrynet/foundryvtt/issues/1915](https://gitlab.com/foundrynet/foundryvtt/issues/1915) for details.
- Rename `CONFIG.tokenTextStyle` to `CONFIG.canvasTextStyle` to better reflect the more widespread usage of this text styling configuration among multiple types of placeable objects.
- Factor out some CRUD helper methods for synthetic Token Actor operations into a helper class to help simplify the Actor entity code.
- Refactor `Playlist.howls` to more generically be named `Playlist.audio` as a collection of audio helper objects.
- Redesign the functionality of flushing the chat log to utilize the new deleteMany database operation.
- Restore a server-side validation check on the User entity which requires user names to be unique within the World.
- The Collection.directory static attribute has been changed to an instance attribute.
- The object of IP addresses and invitation links for the game has been renamed both on the server side as well as client side from `ips` to `addresses`.
- Application developers are now able to customize the appearance and behavior of TinyMCE editors by overriding the `_createEditor` method to customize the options passed to TinyMCE initialization.
- Improved `user.targets` as a specialized Set subclass which handles dispatching a Hook event whenever Token targets are changed. See [https://gitlab.com/foundrynet/foundryvtt/issues/1940](https://gitlab.com/foundrynet/foundryvtt/issues/1940) for details.

### Documentation Improvements

- The Foundry VTT developer API documentation has been redesigned to use a new JSDoc approach. The new documentation is available here ([http://foundryvtt.com/api/](http://foundryvtt.com/api/)) and contains far more coverage and improved clarity around how concepts are used and relate to each other.
- Corrected some out-of-date instructions on the Module and System Installation page: [http://foundryvtt.com/pages/modules.html](http://foundryvtt.com/pages/modules.html)
- Added a section on minimum hardware requirements to the Frequently Asked Questions page: [http://foundryvtt.com/pages/faq.html](http://foundryvtt.com/pages/faq.html)

### Known Issues

- A visual artifact exists when first placing a new token that may result in duplicated sprite images for the Token until the canvas is re-rendered.

## Beta Version 0.4.3, 2019-12-15

Greetings esteemed supporters. I'm very excited to share **Foundry Virtual Tabletop - Beta 0.4.3** which is an incremental release which makes the 0.4.2 major release available to all Patreon supporters while adding a number of improved features and bug fixes to the software.

The major focus area for **Beta 0.4.2** was Audio/Video chat integration, AWS S3 integration, the Token targeting system, and improvements to Journal entries. The **Beta 0.4.3** update iterates and improves upon those changes by correcting several bugs and further polishing those features. If you have not yet familiarized yourself with them, I strongly encourage you to read the Beta 0.4.2 Release Notes.

The most exciting addition in 0.4.3 is the availability of a **standalone MacOS application** which is an exciting milestone that allows MacOS users to have the same native Electron experience that Foundry VTT game-masters on Windows and Linux can enjoy.

Together, updates 0.4.2 and 0.4.3 comprise a really comprehensive update which touches and improves upon a lot of systems, I sincerely hope you all enjoy it. Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- The software now has a working native application build for MacOS! This is a big milestone which has been long overdue. I am really excited for the Mac users out there to have the option of using the software directly through Electron in addition to the ability to run a Node.js server. See the update page for download links for the native Mac application. Please note that the app is not code signed (at this time), so you will need to authorize that you are willing to trust the software in order for MacOS to allow you to use it.
- The Electron application will now launch in fullscreen mode. Added support for a keyboard shortcut to toggle Fullscreen mode for the Electron app: `F11` for Windows and Linux, and `Ctrl+Cmd+F` on MacOS.
- If requesting an Entity or Compendium entry by name or ID as a Roll Table result, the name field will now be automatically cleared if the requested target does not exist.
- The included version of Font Awesome has been upgraded to version 5.12.0 including many new and updated icon characters.
- Improved the flexibility of the new Token Targeting tool in the Controls palette. The tool now allows for clicking directly on tokens to target them individually in addition to rectangular selection for multiple Tokens. Shift+click while using the Token Targeting tool will remove a Token from the targeted set.

### Core Bug Fixes

- Fixed an issue which prevented Map Notes and Tiles from being dragable.
- Fixed an error resulting from a missing permission assignment for newly created Users related to the deprecation of the permission property in the User data model.
- Improved the permission control for users with LIMITED permission to a Journal Entry to ensure that they can only see the image for the entry and not it's text content.
- Fixed a problem in the A/V module which displayed control buttons to force disable/enable the video and audio channels of a fellow GM user, despite that action not being supported by the software.
- Fixed a UX problem with A/V involving cycling the camera sizes of other broadcasters in the call while your own camera was disabled - producing inconsistent video sizes once your feed was re-enabled.
- Corrected an issue with the Setup screen, where the available file storage backends were not provided to the client - resulting in the File Picker ui not being usable for things like selecting a World background image.
- Fixed an issue with dynamic entity links drag+drop in rich text editors which was not properly working for certain Entity types (Scene, Journal Entry, and Roll Table).
- Resolved an edge case failure mode with Roll Tables where, if the only unlocked results lay outside of the possible range allowed by the dice formula - resulting in an infinite loop attempting to retrieve a valid result.
- Fixed a problem with Roll Table results where, if two Entities of the same type have the same name, they could not be differentiated even using their IDs as references.
- Corrected a UX issue with Roll Tables where unsaved changes in other results could be lost when changing the Result Type dropdown selector.
- Fixed a networking problem in the EasyRTC library by explicitly bundling a patched version of that code with Foundry VTT until an upstream merge request is completed which would allow returning to the standard Node.js library.
- Resolved an error in the Token HUD which caused the target token button to throw some console errors related to toggling the CSS class of the HUD display.
- Added some missing localization strings for the Target Selection tool and Roll Table features.
- Fixed an issue with scrollbars while editing long-form text in the rich text TinyMCE editor.
- Corrected a rendering issue for hexagonal token borders for a subset of hex grid orientations.

### Core Software, APIs, and Module Development

- [POTENTIALLY BREAKING] The `Item.id` getter will now return the `data.id` property of an Owned Item if the item instance is owned by an Actor, and the formal entity `data._id` otherwise.
- Modified the cadence with which UPnP requests a renewed lease on the port mapping. Previously this occured every 30 minutes, but this occasionally resulted in expired leases, so the timer has been reduced to 5 minutes while the FVTT app is running.
- Added an explicit `Actor.prepareData()` call `during _createOwnedItem` and `_deleteOwnedItem` handler workflows to ensure that Actor data which depends on the items that Actor owns is re-calculated correctly.
- Implemented a CI/CD build and deployment pipeline to automate the build and release process for Foundry VTT. Many thanks to Toon324 from Discord for his assistance and advice with this process.
- Added new helper methods of `Dice.minimum(formula)` and `Dice.maximum(formula)` which help to understand the minimum and maximum results which can possibly occur for a certain dice formula.

### Documentation Improvements

- Updates to the overview of implemented and planned features: [http://foundryvtt.com/pages/features.html](http://foundryvtt.com/pages/features.html)

### Known Issues

- None at this time.

## Beta Version 0.4.2, 2019-12-10

Greetings esteemed supporters. I'm very excited to share **Foundry Virtual Tabletop - Beta 0.4.2** which is a major release that adds significant new features, functionalities, bug fixes, and API tools to the software.

The major focus of this update has been **audio/video chat integration** for group voice and video chat directly within FVTT. This work is the result of an exciting collaboration between myself and [KaKaRoTo](https://www.patreon.com/kakaroto) who prototyped much of the underlying technology through his excellent "Arcane Viewing" module. We partnered together to adapt that approach, add new features along the way, and integrate it seamlessly with the core Foundry Virtual Tabletop software.

A second exciting technological innovation in this Foundry VTT update is integration for **AWS S3 integration** as an available file browser location. This allows you to connect your Foundry Virtual Tabletop client directly to an S3 account to browse content stored in the cloud and even upload new content directly to your bucket.

Other exciting additions include the addition of a **Token targeting system** which allows you to designate specific Tokens as the targets for your abilities, more flexible Entity linking as part of the **text editor and Journal system**, improvements for **Measured Template rotation**, and a new **Self Roll** dice rolling option.

Overall, I'm proud of this comprehensive update which touches and improves upon a lot of systems, I sincerely hope you all enjoy it. Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- Audio/Video chat for voice and webcam support has been added directly within Foundry VTT. This work is the result of an exciting collaboration between myself and [KaKaRoTo](https://www.patreon.com/kakaroto) who prototyped much of the underlying technology. We partnered together to adapt the prototype, add new features, and integrate it seamlessly with the core Foundry Virtual Tabletop software. Please note that in order to enjoy the benefits of A/V integration in your game, you will need to satisfy some specific criteria for your hosting environment, most notably running the server using an SSL certificate. For more details on the technology behind A/V integration and how you can use it in your games, please read the documentation page here: http://foundryvtt.com/pages/features/av.html
- Added server-side support for AV signaling and Turn servers to empower the WebRTC networking approach as a built-in feature.
- Added a client-side WebRTC framework with a client implementation using the EasyRTC library and a suite of A/V related configuraton settings.
- Added an AV configuration menu, accessible from the Settings Sidebar which allows you to configure the A/V settings you wish to use within your World.
- Added a **Token Targeting** system which allows you to designate a Token or Tokens as your current Targets. The core system implementation of this feature does not necessarily do anything with this target, but it provides a framework for users to indicate a Token as a target which is a pivotal step towards allowing systems and modules to build exciting new automation features which automatically resolve attacks or abilities against the designated targets. Double right-clicking a token you do not own will mark it as a target. For tokens you do own, right clicking will activate the HUD and a toggle option in the HUD allows you to mark that Token as a target. Additionally, there is a new Target tool in the control palette which allows you to left-click to mark specific tokens or groups of tokens as your targets. Holding the SHIFT key while marking targets will add or remove targets from the currently marked set.
- Added integrated support for AWS S3 file storage which lets you use an AWS account and S3 buckets as a built-in browseable and uploadable storage location for media assets that are used within Foundry VTT. To enable this functionality, you must include an entry in your options.json config file which points towards another JSON file that contains your AWS credentials. If such a file is correctly specified and the AWS user has permission to access S3 buckets, those buckets will be available for use in the File Browser for players who are allowed to use it. For examples of how to configure AWS S3 access and how to restrict permission for that access to specific buckets, please see the documentation here: http://foundryvtt.com/pages/features/aws.html
- The default/recommended user data location for Linux users `/home/$USER/.local/share/FoundryVTT` was not available on certain Linux images where the .local directory did not exist. The software will now attempt fall-back default locations of `/home/$USER/FoundryVTT` and `/local/FoundryVTT` if prior options are unavailable. You can manually override this location to any destination of your choosing using command-line flags or environment variables. Please consult the documentation here: http://foundryvtt.com/pages/hosting.html#where-do-i-put-my-data
- Placed Measured Template objects can now be easily rotated by hovering over their control icon and using CTRL+Wheel (for slow turning) or SHIFT+Wheel (for fast turning) relative to their point of origin. This greatly increases the convenience of placing and positioning Cone and Ray type templates.
- A small change to the Wildcard Token algorithm allows it to generate more variety in placed tokens. The algorithm is no longer totally random, taking into consideration the last token placed to avoid drawing chains of duplicates. This should result in more variability in the appearance of groups of Tokens which used a wildcard selector.
- Added a command-line option to disable using UPnP to automatically request port forwarding. Passing `--noupnp` as a command-line flag, for example `node main.js --world=myworld --noupnp` will start the application while disabling UPnP support.
- Added significant improvements to dynamic Entity linking in Journal entries and other rich text fields. These improvements support several enhancements. Firstly, entities may now be linked directly by their id attribute instead of by searching for their name, for example `@Actor[kjsfd923jisdf]`. Secondly, every linked Entity may be explicitly renamed with curly-braces which follow the square-braces that identify the Entity, for example `@Actor[kjsfd923jisdf]{Tim the Sorcerer}`. Lastly, entities may now be linked directly from a compendium pack using the following syntax `@Compendium[collection.id]{Custom Name}` where packName and id are replaced with the collection and id values of the entity being linked.
- As a complementary feature to the new expanded Entity linking system, you may now drag+drop any Entity into an active rich text editor and it will automatically create a dynamic Entity link for you using the dropped entity's data.
- As a final valuable feature for new Entity dynamic linking, the links for Actor type entities can now be directly drag+dropped onto the game Canvas to instantly create a Token for the linked Actor, giving Game Masters a helpful way to plan ahead for combat or social encounters.
- Improved the aesthetics of the Token visual border by moving it beneath the token artwork which now clips over the border as the token is rotated around it.
- Added a hex-grid specific token border for tokens which have width and height both equal to 1 (in other words, a single hex). For Tokens which do not occupy a single hex, they still receive a square or rectangular border - at least for now, but for those of you using Hex maps this should improve the visual appeal of your hexagonal tokens significantly.
- Add string trimming to the package.json manifest files used to install game systems or modules to automatically remove leading or trailing spaces which were a common source of failure to install a package where a space cause the provided URL string to be incorrect.
- Clicking on an Entity in the sidebar whose sheet is already rendered, but minimized, will maximize the existing sheet instead of doing nothing.
- Added a new roll-mode option, the **Self Roll** which allows you to privately roll a dice formula where the result is only visible to the roller. Other users are notified in the chat log that dice were rolled, but they cannot see the result. Self rolls can be manually placed using the `/selfroll` or `/sr` prefixes, for example `/sr 6d6`.
- Added a feature to support unsnapped ruler measurement on otherwise gridded maps. Holding SHIFT while measuring with the Ruler will show distances which are calculated point-to-point, rather than as a function of the number of grid spaces traversed by the measured path.

### Core Bug Fixes

- Identified and fixed a significant performance-inhibiting issue with light-emitting tokens and line-of-sight polygons. The intention of the sight system was that when a Token which emits light moves on the map, it's LOS and FOV polygons are updated and replaced in the rendering of the Sight Layer. What was happening instead was that each token movement was generating a new FOV polygon which was stacking on top of the previous ones for the purposes of collision and visibility tests. This could gradually degrade performance over the course of game sessions. Thanks to Sky from Discord for noticing a peculiar Token behavior which led to the identification of this issue.
- Solved a potentially serious issue which caused an active world to be deactivated when a user in Chrome navigated towards their game URL and was prompted with a hint of visiting the /setup page. Since Chrome pre-caches pages using GET requests, if you were a GameMaster user, simply typing the address in the navigation bar would submit a GET request to the setup page, resulting in your current world being deactivated. To resolve this problem, the deactivation of worlds has been changed to a POST request which can only be submitted from within the currently active world. A new helper function `game.shutDown()` has been added to assist with this workflow.
- Newly created Users were incorrectly receiving an initial role of NONE, instead of the intended starting roll of PLAYER. This has now been corrected.
- Fixed a bug which prevented activating the Token HUD in cases where the Token no longer had a valid Actor assigned.
- Resizing an Application window previously stored the unconstrained height and width after the resizing operation, but this ignored any minimum dimensions which were enforced by CSS. Now the constrained dimensions are stored instead.
- Changes to the User's display color did not previously immediately take effect for the Ruler display. This is now corrected and changes to the color choice will immediately change the ruler appearance.
- Journal Entries to which the User only has LIMITED permission are now restricted and not visible in the sidebar, as originally intended by the Journal system. These entries can still be seen as map pins where their icon, title, and image are visible - but their text cannot be read unless the player has OBSERVER or greater permissions.
- Changing the Actor Link state of a placed Token was not correctly updating that Token's Actor reference, resulting in the Token still updating when the original actor was changed.
- Resource bar values were not correctly displayed on the Token Configuration sheet unless the attribute target was first changed. The current and maximum values of the bar's attribute will now be showed on the Token config sheet, although they cannot be edited there.
- Changes to the title of Journal Entries now propagate to all Map Notes which referenced that Journal Entry. Previously only the first Note was updated while others remained on the old title.
- Text written in Journal Entries may now be selected with the mouse cursor so it can be copied and pasted elsewhere.
- Fixed a bug which caused the "Show Artwork" feature for an Actor to result in an infinite loop due to nested JSON structures.
- Solved a problem with undefined flavor messages for dice rolls in chat log export to text files.
- Corrected a problem with Wildcard Token paths resulting from the new User Data location. Wildcards should once again work as expected!
- Fixed an issue which caused `Roll.toMessage` to produce a duplicated dice roll sound effect in the case of blind rolls.
- Resolved a problem with starting the Electron application using the `--world` command line flag which failed to properly wait for world setup to complete before attempting to load the localhost URL in the app.
- Improved the permission check for writeability of the User Data parent directory to test for the user data directory directly if it already exists.
- Improved the system or module installation process to avoid displaying NaN% as the progress tracker for packages where there is not a total number of bytes returned in the zip file header.
- Fixed a version number comparison issue related to core migrations when moving across major versions.
- Attempting to install an invalid system or module incorrectly kept the Setup Configuration buttons all disabled while it waited for the installation to succeed (which it never did). Now those buttons will become re-enabled if an attempted installation is unsuccessful, allowing the user to try again with corrected input.
- Fixed a failure with the generation of Scene thumbnail paths due to file path changes related to the new User Data location. Scenes which failed to have a thumbnail generated will need to be re-saved to correctly produce the thumbnail. Follow this process: (1) open the Scene Configuration sheet, (2) remove the existing background image and Save, (3) restore the background image and save again. This second save will generate the correct thumbnail image. Future scenes will not encounter this problem.
- Solved a new (returning?) problem in the File Picker related to spaces in folder paths.
- Improved the behavior of drag+drop Token placement on hexagonal grids. Previously a bug would often result in Token placement at the vertex of hexes, rather than in the center of a hex. This should be eliminated and drag+drop token placement for hex grids should work intuitively.

### Core Software, APIs, and Module Development

- **[BREAKING]** A change to the `Entity.prepareData` function now allows for entity properties to be used during data preparation as the data object is first assigned to the instance, and then prepareData operates upon the assigned data instead of pre-processing the data before assignment. As a result, if you define custom `prepareData` calls in your game system their signatures will need to adjust.
- **[POTENTIALLY BREAKING]** The socket handlers for Owned Item updates did not previously re-prepare data for the owning Actor entity. This resulted in cases where the Actor's prepared data *should* change as a result of changes to it's items, but those changes did not occur automatically, forcing some module or system authors to manually re-prepare Actor data. This now does happen automatically as part of the aforementioned changes to prepareData. As a result, if you were manually re-preparing data for the Actor when an Owned Item was updated, you should no longer do that.
- **[BREAKING]** The text editor helper functions have been factored into a namespaced class, `TextEditor` which centralizes logic related to TinyMCE and other rich-text features. The previous methods of `createEditor` and `enrichHTML` are now deprecated in favor of `TextEditor.create()` and `TextEditor.enrichHTML()`. Support for the old function names will be removed in 0.5.x.
- Added support for generic rendering hooks for certain applications which provide fundamental abstract versions. Initial support exists for `SidebarTab`, `ActorSheet`, and `ItemSheet` classes. Registering a render hook, for example `Hooks.on("renderActorSheet", (app, html, data) => {});` will now fire for every subclass of `ActorSheet, allowing you to determine in your event handler when or how to respond without needing to learn the exact class names for which to listen.
- The concept of `gridPrecision` has been moved into the options object for each CanvasLayer.
- The set of file storages which are available for use in the file picker are now passed from the server as part of the initial data dump.
- The "type" attribute for input HTML tags is now allowed in cleaned HTML input, allowing input elements to be used in chat messages, among other places.
- The underlying interface for a valid `FileStorage` has been factored out to allow for multiple implementations of different file storages. The AWS support is one such implementation, as is local file storage on your host machine. This pattern could be extended in the future to allow for file storage support from other cloud data storage providers.
- Added a `FormApplication.submit()` method which wraps the form processing and submission process while allowing for additional external data to be added to the update. This enables for joint workflows which process unsaved changes in an open FormApplication instance while adding some additional specific changes from external triggers.
- The PIXI library has been updated to major version 5.2.0. You can read the PIXI release notes for this version update here: https://github.com/pixijs/pixi.js/releases/tag/v5.2.0
- The index mapping for a Compendium pack is now locally cached once `getIndex()` is called once for the pack. This helps to avoid unnecessary DB traffic and also makes Compendium-linked entity links work more effectively.
- Added an optional `Entity.compendium` flag which allows for easily tracking which Entity instances belong to a Compendium vs natively belonging to the active World.
- Added the `User.permissions` object to the User data model which allows for more fine-grained key-value pairs of permission abilities granted to a specific User. This is used now for A/V permissions to enable broadcasting, but will be used for more use cases in the future.

### Documentation Improvements

- Added overview page for the User entity: http://foundryvtt.com/pages/entities/user.html
- Expanded the detail provided on the API documentation for the User entity: http://foundryvtt.com/pages/api/entities/user.html#userapi
- Added an overview page for the Item entity type: http://foundryvtt.com/pages/entities/item.html
- Added instructions page for Audio/Video Communication features: http://foundryvtt.com/pages/features/av.html
- Added instructions page for AWS S3 Bucket configuration: http://foundryvtt.com/pages/features/aws.html

### Known Issues

- The push-to-talk button does not currently work as a push-to-mute button for "always" and "activation" broadcast modes as intended. This feature was planned and scoped but not quite completed in time for 0.4.2 release.
- Currently the push-to-talk button can only be a keyboard key, but adding support for a mouse button will come in the next update.

## Beta Version 0.4.1, 2019-11-20

Greetings esteemed supporters! I'm thrilled to be back with yet another Foundry Virtual Tabletop Beta release with Version **0.4.1**. You are perhaps wondering why this release comes so soon after the previous 0.4.0 update. I am pursuing a new update strategy between now and release which I hope will provide a smoother experience for testers in both the Council and Beta supporter tiers. Effective immediately, even numbered release (for example 0.4.0) focus on large changes and more meaningful feature additions. These even numbered releases will be made available to the Council tier only for a period of 5-7 days, at which point an odd-numbered release (for example 0.4.1) will release for both Council and Beta including a number of fixes, adjustments, and improvements related to the prior release's additions. As such, this 0.4.1 update is available immediately for all tester tiers as it resolves and improves upon a number of the limitations and weaknesses of last Friday's 0.4.0 release.

The focus of this update is bug fixes, tweaks, adjustments, and stability improvements to the 0.4.0 release from last week. There are a number of bug fixes, as well as some feature changes in response to user feedback. There is also a new D&D5E system update (version 0.71) which adds some cool new features as well as fixes and changes from last week's version.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- The most significant failure of the initial 0.4.0 release was the lack of a configurable setting for where user data, which is now stored outside the application installation location, is persisted. This was a misstep on my part as I failed to anticipate the many cases in which lack of configurability for this location is a critical concern. Thank you all for your honest criticism of this limitation. I'm pleased to say this is far more flexible in 0.4.1. There are three ways that you may customize the user data location:
- 1. A command line flag `--dataPath={path}` when the application is started.
- 2. An environment variable `FOUNDRY_VTT_DATA_PATH`.
- 3. An `options.json` configuration override in the default OS location for user data using the `dataPath` key which redirects to an alternate location.

- Documentation for these three usage modes is available in the GitLab issue https://gitlab.com/foundrynet/foundryvtt/issues/1672 and on the updated documentation page here: http://foundryvtt.com/pages/hosting.html#running-the-application
- Users are prevented from installing packages (systems and modules) which require a minimum core software version greater than the VTT version they are currently running. They will be notified upon attempting to install such a package that they must first update their core software.
- The package installation process now validates the type of package the user is attempting to install. Previously this could result in a user incorrectly attempting to install a system as a module, or vice versa. Incorrect usages will trigger a notification which informs the user of their error.

### Core Bug Fixes

- Corrected a logical flaw which could result in multiple Gamemaster users being created for a world each time the server was started, resulting from the software (incorrectly) believing that the world had no active GM tier user.
- Resolve an incorrect async usage which could result in the Electron window trying to load the application before the Express server had begun listening on the target port.
- Ensure that SSL certificate and key paths are resolved relative to the Config subdirectory within the user data location. Absolute paths to other locations may also be provided.
- Resolved a bug which would cause all the door controls on a Scene to be temporarily visible when resizing the window (for example when pressing the ALT key on Firefox).
- Corrected a problem with the Combat Tracker which prevented tracked resources from being updated in real time when the values of those resources changed on the combatant's Actor (or Token).
- Fixed a problem with automatic playback enablement for ambient audio sources when a user interaction is first observed. Now ambient audio will begin playing automatically once an interaction occurs.
- Remove uses of `Object.fromEntries()` which is not well supported by all modern browsers.
- Fixed several JSDoc syntax errors throughout the code which prevented documentation files from building properly.
- Correctly display the numeric value of the Ambient Light Source opacity slider when it is adjusted in the configuration sheet.
- Fixed an issue which could cause the initial permissions check for the user data directory to fail if the parent of the requested data directory does not exist. This check now occurs as an earlier explicit validation to ensure the user data location can be reached.
- Direct updates to an Actor entity items array failed to rebuild the `actor.items` array of Item instances. This is now handled in the onUpdate logic of an explicit array of items is directly provided to the parent Actor update method.

### Core Software, APIs, and Module Development

- Added flexibility to the `Application.setPosition` function to allow for callers to explicitly request height as "auto".
- Add an `invertObject` helper method which can swap the keys and values of an object. This does not incorporate safeguards to guarantee that the initial object is 2-dimensional or that it's values are unique. The user of the function bears the responsibility to provide the correct type of input.

### D&D5e System Improvements (D&D5e release v0.71)

**Note now that the D&D5E system is no longer automatically bundled with the core VTT software, you must manually update the D&D5E system from the setup panel as you do with other modules and systems.**

- Introduce a dialog displayed when casting a prepared spell which consumes a spell slot that prompts the user to select the spell level at which they wish to cast the spell. The available choices are all levels greater than or equal to the normal level of the spell for which the character has at least one maximum spell slot. You are only able to select a level at which to cast where you have one or more spell slots remaining to spend. When the chosen spell level is confirmed, the spell slots counter for the chosen spell level will be automatically deducted. A checkbox allows you to bypass this requirement and cast the spell without actually consuming the spell slot. When casting a spell from the character sheet, SHIFT+Click will bypass the level selection dialog and skip directly to casting the spell at it's minimum allowable level. Please note that damage scaling from upcasting spells is not yet automated as part of this enhancement - this is a phase one which implements the spell level selection and automated consumption of spell slots. Applying damage scaling formula automatically for upcast spells will be included in the next 5e update.
- The Saving Throw button displayed in chat item cards enables all players (both the original user of the item as well as other players) to quickly make saving throws as necessary. A saving throw of the appropriate type will rolled for your currently controlled Token. SHIFT+Click on the Saving Throw button will bypass the dialog for choosing advantage/disadvantage or applying additional modifiers.
- Improved automatic migration functions for pre-0.4.x worlds in several ways.
- - Added more explicit migration support for Scenes and Scene-type world compendium packs to handle Tokens in those scenes which have actorData overrides applied that also need to be migrated.
- - Fixed a temporary problem immediately after migration where some data in the currently viewed Scene would still appear incorrect, even though the underlying data had correctly migrated.
- - Fixed an issue with armor type migration which should now properly persist the armor type of Equipment items if they were labeled in a way that matches the config enum.
- - Improve handling of deprecation migration for unused fields to ensure those fields were not explicitly updated by some prior migration.
- - Improve the logic for weapon item migrations to avoid exiting early if weapon property flags were not set, which resulted in bypassing other migrations which still should have occured.
- - Fixed migration issues for Tokens in Scenes which point to an Actor ID which does not exist.
- Restored the correct healing formulae for healing potions in the Items SRD compendium pack.
- Improve the automatic sizing of item sheet dimensions. The size of the Descriptions tab will remain the same, but the Details tab will be more adaptively sized up to a maximum allowable height, beyond which scrolling is required.
- Compress the sizing and dimensions of the character and NPC sheets slightly to better accomodate small viewport devices (specifically 768px height). The new character sheet clocks in at 732px height down from 780px previously.
- Fix several character sheet bugs introduced with the 0.4.0 update including:
- - Inventory item weights only showed the weight for a single item, rather than the weight of the full stack in cases where quantity > 1.
- - Removed starting/default values for character race and alignment, these fields will now simply begin as blank.
- - Removed the incorrect +2 initiative modifier which newly created Actors were automatically starting with.
- - Removed the "rollable" tag from the Health attribute on Player Character sheets which incorrectly indicated that it could be clicked upon.
- - Fixed the ability to expand and display in chat player class levels from the Features tab.
- - Fixed the labels for skill and ability check dialogs which previously were pulling undefined strings.
- - Corrected the behavior of the currency converter button which now works as intended.
- - Display zero charges when an item with a maximum number of charges has none remaining as was intended. Previously empty items were incorrectly not showing charges at all.
- You may now copy text from an item card displayed to chat by the 5e system. Previously this text was not selectable.

## Beta Version 0.4.0, 2019-11-15

Greetings wonderful supporters and friends. Today marks a significant milestone for Foundry Virtual Tabletop as the software moves into the 0.4.x version on the path towards release. This is a major update version which evolves the software in some very significant ways. In addition to the update notes, there are some critical changes to the installation and usage of the software which are detailed in the post containing the download links for the software. Please be sure to read those notes carefully as well.

This update is a generational step investing in the underlying infrastructure of the software. As a consequence of that, most of the big new features in 0.4.0 deal with underlying features, networking, application structure, and data structure. This results in relatively fewer big client-side changes this time around, but I want to make sure everyone understands how the technical investments made in the 0.4.0 launch are critical to empower further growth for the platform.

The biggest gameplay-altering feature in the 0.4.0 update is a **major update to the D&D5E system** which almost completely overhauls and expands the system data model to empower more robust data stored on every actor and item as well as an entirely new interface and design for Actor and Item sheets. In addition to 5e improvements, the **Simple Worldbuilding** system has been redesigned to offer more flexibility as a system agnostic toolkit which is compatible with the 0.4.x release.

Thank you all for appreciating my work, providing thoughtful feedback, and for your patience during this update cycle which I realize is more disruptive than usual.

### New Features

- New more strict version control limitations exist on game systems and add-on modules. These packages should define a minimum core version in their manifest file which, if a module or system becomes too out of date to be compatible with the core software, it will be automatically disabled. Worlds which depend on a system which has become disabled or is otherwise unavailable will not be able to be loaded until a system update is applied. I will be adding a mechanism in an upcoming update to allow users to manually override this restriction and opt-in to continue using outdated modules at their own risk.
- In order to comply with application code signing requirements (code signing is not yet implemented, but eventually will be) user data must be moved outside of the application installation directory itself. In many ways this is a downgrade for user experience, where it was highly convenient to have all of the VTT data in a single place inside the application public folder. The initial solution in 0.4.0 is to use the recommended/authorized location for user application data in your operating system. For Windows this location is `%localappdata%/FoundryVTT`, for MacOS `~/Library/Application Support/FoundryVTT`, and for Linux `~/.local/share/FoundryVTT`. I realize these locations may not be ideal for many of you, especially given the need to store a large amount of image, audio, and video content for use inside the VTT. I will be actively working on a way to make this location customizable as part of the next update.
- Due to the new separation between bundled public assets and custom user data, the File Picker interface has also evolved to feature tabs at the top for switching between different source data locations. Currently you can switch between User and Public, with an extra placeholder tab for S3 data - an upcoming feature that will be added in a future update.
- Added an optional game setting to disable the auto-pan to a speaking token through the chat bubbles system.
- Added support for each User entity to have an image avatar. This avatar is not widely used within the VTT yet but will be more broadly utilized for other upcoming features. The User avatar is configured in the player config application.
- Improved upon the light source tinting addition in 0.3.9 by moving that layer beneath fog of war and causing it to more proactively update in the face of other changes to the scene (like walls and doors).
- Added a new optional server configuration to assist with users with a reverse proxy or DNS name associated with their VTT instance. Setting the `hostname` field in the `options.json` file will allow any external links to the VTT to be generated using the correct hostname instead of the public IP address.
- Added a new optional server configuration to allow for serving the VTT from a non-root path within the host. Setting the `"routePrefix"` option to some string value in the options.json file will cause that prefix to be used. For example, setting the route prefix to "demo" would cause the application to be served from your.ip.address:30000/demo/game.
- The join screen has been refactored to involve more aspects of a client-side app instead of a static template rendered by the server. This allows for some dynamic interactions with the join experience like success or error notifications for login attempts or other helpful prompts.

### Core Bug Fixes

- Resolved a security loophole which could allow users to upload and browse files outside of the allowed public (and now user data) locations by abusing relative path traversal syntax.
- Fixed a bug which caused players to see a blank image for for a journal entry if no image was set instead of the text view when text content was present.
- The Actor sheet tried to be helpful by automatically setting image artwork for an Actor's prototype token using the actor profile image if no token artwork was set. This failed, however, when both the profile image and the token image were updated (to different values) in the same API call.
- Fixed a bug which prevented whispered messages from being visible to the original sender.
- Allow for raw `data://` to be a valid URL scheme which was previously stripped during server-side HTML sanitization.
- Fixed a very problematic bug which allowed a Folder to become referenced as it's own parent, creating an infinite recursion during sidebar rendering.
- An error caused old token `actorData` overrides created when a Token was not linked to its parent actor to continue to be applied even once the Token data was linked.
- Addressed a problem which caused the area of effect for created light sources to be displayed to players instead of just the creating GM user.
- Changes to expectations around provided SSL certificate paths caused users who were previously providing an absolute path to their certificate to no longer detect SSL mode. Absolute paths are now supported in addition to relative paths. Note, however - that a bug related to this still made it into the 0.4.0 build, so a portion of this fix suffered from regression with the new user data location changes.
- Modifying walls (including opening and closing doors) did not correctly cause the visible light from a color- tinted light source to update it's displayed polygon. Now wall changes will correctly trigger refreshes to dynamic light source FOV polygons.
- Fixed a problem in the server side socket handling workflow which could result in failed server-side socket handlers broadcasting their error messages to all users, not just the user which triggered the failed request.
- Corrected problems with Playlist updating when the playing field of the parent playlist data model is altered. This relates to an issue with the `playlist.stopAll` API which was not correctly terminating playback for all tracks within the stopped playlist.
- Fixed some edge case issues with certain very large token limited visibility angles which caused the resulting points of the LOS polygon to not be properly sorted by origin angle.
- Fixed a defect which prevented player-level users from being able to interact with the Combat Tracker to add or modify initiative rolls.
- Corrected a problem with new User creation which could fail to refresh the visual display of the Players Configuration application unless the client was refreshed.
- Added an (intended) restriction to the set of Entity types which can be referenced in a RollTable to the same set which can be also added to a Compendium pack.
- Prevent executing a roll for a RollTable which contains no possible results.
- Fixed an issue RollTable results resetting their content to empty or default values when a select dropdown for the result type was changed.
- Fixed defective CSS rules for the updated combat tracker which resulted in large artwork for each combatant.
- Addressed a problem which caused the update notes to not properly display when using the built-in updater.
- Fixed a CSS rule which was preventing highlighting of text data in chat messages. This now allows the content of chat messages to be selected for purposes like copy+paste.

### Core Software, APIs, and Module Development

- [FUTURE BREAKING] There have been major changes to the schema for `template.json` files included with game systems which define the data structure for the Actor and Item data model within those systems. Systems which are using the old template structure will continue to function, but the new template schema is strongly recommended and can be enabled by setting `"templateVersion": 2` in your system.json manifest. By version 0.5.x all templates will be assumed to be "version 2" and support for v1 templates will be removed. Read the following issue for much more detail and example template structure: https://gitlab.com/foundrynet/foundryvtt/issues/1614. You may also refer to the updated D&D5E and Simple Worldbuilding systems which implement the v2 template specification.
- [BREAKING] Modules and systems which have not been manually updated for compatibility with 0.4.0 will not be flagged as outdated and not able to be used until they are updated. The only thing you MUST do is to add minimumCoreVersion as 0.4.0 to your module.json for the system to recognize it as updated.
- [BREAKING] The template loader will now load HTML template paths from the user data location if their path is prefixed with the key words of "system", "module", or "world". Otherwise templates will be loaded from the core templates location. A consequence of this for module developers which were previously providing HTML template paths beginning with "public/systems/..." or "public/modules/..." should remove the "public/" component from the path for their template locations to continue working.
- [BREAKING] Concluded deprecation of the old global namespace constant variables. Now all shared client/server constants must be referenced from the `CONST` object. For example `CONST.ENTITY_TYPES` rather than just `ENTITY_TYPES`.
- [BREAKING] As part of improvements to the permission system, `User.permission` has been refactored to `User.role`. This is helpful because it is more semantically consistent with the purpose for this field and it differentiates its usage from `Entity.permission` which is used on other entity types for a different purpose. References to `user.permission` should be updated to target user.role instead.
- ES6 style code modules are now directly supported! Instead of specifying `scripts: []` in your module and system manifests you may specify `esmodules: []` which provides a set of paths to ES6 module entry points. See https://exploringjs.com/es6/ch_modules.html for more information about ES6 modules and see the new D&D5E system for a working example of an entire game system which is built as an ES6 module instead of as a single JavaScript file.
- Added a new flag for debugging Hook functions. Setting `CONFIG.debug.hooks = true` will display logging information for every hook which is called with the arguments passed to any hooked functions.
- Server side user authentication and cookie management functions have been refactored out as a separate module for better code maintainability.
- Removed usage of session-based storage in favor of the simpler cookie-based approach. Session storage was used pretty poorly by the software, and had a bad match rate of connecting client cookies with pre-existing sessions, furthermore it became challenging to anchor the same session information for both the HTTP request in Express and the Socket.io request. I have simplified the system in several ways by removing session storage, by passing the user's cookie to the socket initialization, and by linking identity for both socket and HTTP requests. This new approach can upgrade gracefully to add back a persisted session storage in the future if it is deemed to be value adding.
- Added a server-side socket handler and client side method which allows users to request a full data migration of a Compendium Pack to the latest system data model. This tool can be valuable for module developers or users who fear their compendium data has become broken in some way. For a given compendium pack, the client side API is `pack.migrate(options)` which causes the server to update all entities in the compendium, ensuring their data model is accurate.
- The parsed and structured system data model is now passed to the client for reference so that modules and systems can use it client-side to make data adjustments or create new entities. See `game.system.model` to inspect the data structure.
- Electron has been updated to new major version 7.0.0 incorporating node.js updates and several new features.
- The widely used `mergeObject` utility method has been improved to support a means for removing keys from the target object during the merge process. This involves a special syntax like the following: `mergeObject({a: 1, b: 2}, {"-=a": null});` which will result in an object where the key "a" has been removed. See https://gitlab.com/foundrynet/foundryvtt/issues/1625 for more details.
- The `mergeObject` function also supports a new optional argument enforceTypes which is a boolean which allows the data type of the original object to be changed (if false) or raises an error if the data type would be changed (if true).
- A new `Entity.unsetFlag(scope, key)` method has been provided to delete a custom flag that was added to the data model. Previously flags could be added and updated, but not deleted, forcing users to set old or unused flags to some other value like null.
- For children of the FormApplication interface, unfocus events on checkbox type input fields will no longer trigger a form submission.
- Added a new `setup` hook which fires in-between `init` and `ready` events during the VTT initialization process.
- [BREAKING] The arguments provided to the `renderChatMessage` hook was inconsistent with the args provided to other render hooks. The signature has been updated to `(app, html, data)` as with other render hooks.
- [BREAKING] Concluded work to deprecate the old object-style input for ContextMenu instances. Any ContextMenu instances still using the Object style input will no longer function and must migrate immediately to use an Array as the input type of menu options.
- Add some extra checks to prevent folders which are already at the maximum folder depth from being seen as valid drop targets.

### D&D5e System Improvements

- The 5e system has been almost totally redesigned in order to feature a new structure as an ES6 module, a new data template which uses the new core template features. An expanded and modified Actor and Item data model to incorporate much more information in a more direct format, and many other new features.
- The above changes involved significant alterations to the D&D5e data model. Please consult the compiled model structure in game.system.model to see the new schema which should be used for D&D5e Actors and Items. Furthermore, please inspect the included migrations module in the D&D5E repo and available as within the API as `game.dnd5e.migrations` for a variety of helpful functions which help to migrate existing Entities and illustrate the changes which occured to the data. For module developers working in the D&D space, I strongly encourage you to connect with me on Discord for any help you need in updating to this latest data specification.
- Many fields in the data model which were previously used are now deprecated and will be removed by Foundry VTT version 0.5.x. These fields are retained in the data model for now, but flagged with a _deprecated key.
- The character and item sheets have been fully redesigned for a more professional aesthetic with a cleaner and more powerful structure.
- Many monsters from CR1 to CR9 have been incorporated into the Monsters SRD compendium pack.
- A new round of Token artwork courtesy of Stryxin from Forgotten Adventures and creature biographies courtesy of Penelope (Vyrnali) are available for low-CR creatures.
- Core concepts of the 5e system like action type, target type, distance units, activation costs, currency denominations and much much more are now persisted as enumeration objects within the `CONFIG.DND5E` namespace.
- The inventory, spellbook, and features tabs for Actor and NPC sheets now have a helpful set of filters which allow you to restrict visibility of the item list to items which have a certain activation cost or usage condition.
- Separate spellbook sections for Innate Spellcasting, Always Available spells, and Pact Magic has been added which no longer uses the same set of spell slots as the spell would if it were prepared normally. This is configured through the "Spell Preparation Mode" field in the Spell Details tab.
- Weapon damage rolls are no longer assumed to benefit from the ability score modifier of their designated ability. While this is usually the case there are many scenarios where this modifier is not granted, therefore the default is that the modifier is excluded from the damage roll unless included with either the a direct attribute reference like `@abilities.str.mod` or the shorthand `@mod` tag.
- Changing an Actor size on the traits tab will automatically adjust the dimensions of their prototype token according to the stated size rules. To set Token base dimensions differently, edit the Actor sheet first then go update the Token size to some non-standard dimension.
- String labels for elements of the data model have been moved outside the data template which is stored on every actor and maintained as system level metadata which is either statically or dynamically computed for HTML rendering.
- All items which can deal damage now support multiple damage types with separate fields for components of the damage formula. Each component of the damage formula may have a different damage type assigned to it.
- Redesigned the use of the versatile damage modifier. The versatile field defines an alternative formula which will replace the first component of the damage formula if the item is used in a versatile way. This level of generalization works well for both versatile weapons as well as for spells like Toll the Dead which deal a different amount of damage in certain situations.
- Added an "other formula" field to all activated items which can specify any arbitrary dice formula that can be rolled in addition to attack and damage rolls. This can be useful for additional damage like poison, for ancillary skill checks or saving throws, or for random results which apply to the effect like for prismatic spray.
- Weapon properties have been migrated from a free-form string to a structured list of boolean flags.
- Spell components have been migrated from a free-form string to a structured list of boolean flags.
- Ability activation cost has been changed from a free form string to a 3 part form featuring a cost type and a numeric activation cost value.
- Spell or Feat effect duration has been changed from a free-form string to a structured field with 2 values; a numeric duration value and a designation of duration units.
- Effect targets have been changed from a free-form string field to a structured object containing a numeric value, a designation of units, and a target type.
- Ability range has been changed from a free-form text field to a structured object with a numeric value and designation of distance units.
- Added support for all physical items to provide a boolean flag for whether or not they are identified as well as a separate text description to be shown in the event the item is not yet identified. This unidentified text is not yet used, but will be adopted in an upcoming version.
- Added support for spell upcasting and cantrip damage scaling. Cantrip damage scaling is already supported with automatic scaling based on character level or NPC spellcasting level (or CR). Spell upcasting is supported now in the data model, with future UI work to allow for automation and selection of the spell level at which to cast a spell.
- Spell saving throws can now accept an explicit spell DC which would override the default formula based on the caster's spellcasting modifier and proficiency score.
- Armor type items may now track the maximum dexterity modifier which can be granted by the piece of equipment.
- Added a new equipment type "trinket" which can be used for items which are equipped and attuned but worn like jewelry rather than used strictly as consumables.
- Localization support has been added for a great many strings used in the D&D5E system. This effort is not complete, but this update goes a long way towards supporting translation for D&D5E into other languages. Please see the file `lang/en.json` in the D&D5E repo for English string keys and translations. Follow the same procedure used by the core software for translating these strings for support in other languages.
- Added an optional attribute for spellcasting level for NPCs so that different NPC creatures can have a specific spellcaster level assigned which may differ from their challenge rating.
- Expand the actor data model to support an optional additive bonus for each skill which, in combination with the multiplicative bonus to proficiency will determine the total skill modifier.
- Added a convenient conversion button to the currency display on Actor Sheets which will upwards convert all carried currency to the maximum allowed denomination using standard currency conversion rules. Electrum counts as 5 silver each (2 per gold). I don't care about your edge cases.
- Limited item uses are now supported for every item type which can be activated. Different limited usage modes are available ranging from per short rest, per long rest, per day, and charge based. Additionally, items can be restricted in use based on a recharge r6 roll which is tracked and automated on the character sheet.
- Trait selector UI now supports a string separator character of a semi-colon (;) which will break a custom trait string to be displayed as multiple tags.
- Added explicit tracking for armor, weapon, and tool proficiencies in the Traits section of the character sheet.
- When adding spells to NPC sheets, those spells are assumed to be initially prepared by default. When adding weapons and armor to NPC sheets, those items are assumed to be equipped and the actor is assumed to be proficient in their usage by default.
- Added an explicit software license (GPLv3) and content license (OGL) files to the D&D5E repository.
- Fixed a bug which casued critical success and failure highlighting to be revealed for blind dice rolls.
- The "Backpack" type item has been renamed to "Loot" to better reflect its intended usage.

### Simple Worldbuilding System Improvements

- Fully redesigned the Simple Worldbuilding system to use the new 0.4.0 data template and ES6 module structure.
- The Simple Worldbuilding system has been split out from the core software as a free-standing open source repo which is open for both community contribution as well as to serve as a helpful boilerplate example for new system developers who are looking for a simple existing template to follow. You can find the worldbuilding system repository here: https://gitlab.com/foundrynet/worldbuilding.
- Actors and Items in the Simple Worldbuilding system can now both support free form key/value attributes which can be flexibly added to their data model. Each attribute can have a data type and label assigned with String, Number, and Boolean (as a checkbox) fields supported.

# Beta Version 0.3.X

## Beta Version 0.3.9, 2019-10-21

Hello Patreon Supporters and friends. I'm very excited to share **Foundry VTT Beta 0.3.9** with you. A lot of work has gone into this update, with 74 issues closed, I'm really proud of the additions that 0.3.9 brings to the Foundry VTT environment. Moreover, the whole update was wrapped up in 2 weeks, so I'm very pleased with the timelines as well. There are a number of big features in this update, some of the key highlights include the addition of **Rollable Tables** as a new Entity type, an expansion of the lighting system to allow for **Color Tinting of Ambient Lights**, an comprehensive overhaul of organizational tools to allow for **manual sorting of Folders and Entities**, and a robust array of bugfixes and API improvements.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- The initial V1 implementation of **Rollable Tables** has arrived! Rollable Tables allow you to define a set of results in a list format, each result has an associted weight and dice roll range. Rolling or drawing fromthe table randomly selects a result based on the table's formula and each result's range. To create a Rollable Table, see the new tab in the sidebar where the icon looks like an indexed list. There are lots of features of Rollable Tables - to cover them all I'll be releasing a Developer Video Update in the coming days, but some highlights include: customizing the weight placed on each outcome, drawing with or without replacement, associating each result entry with an existing Entity or Compendium pack entry, dynamically linking Rollable Tables in rich text, recursive table evaluation for nested layers of randomization, and more!
- Added support for the new RollTable entity as a valid Compendium type, so you may create Compendium packs of Rollable Tables to share wonderful tools for creating random loot, encounters, locations, and more with your players and other game-masters.
- Ambient Light sources may now be provided with an optional tint color. Light source tints are mostly transparent layers with an overlay blend mode which are drawn above the map, tokens, and tiles to cast everything under the lights FOV polygon with a tinted hue. Light source tints can be great for a warm campfire glow or an eerie green flame within a lost crypt. Try them out and let me know how you find them in your game. I will be extending this system to allow for Token emitted light to also be tinted in a future update.
- The /join screen which every player visits when first logging into the VTT has been redesigned! The new join screen offers a custom background, a World description, current players, and the next scheduled session time which can be customized in the configure world menu.
- Improved the styling aesthetics of sidebar directories to feature more clean lines and more clear delineation of which entity belongs to which subfolder.
- Dice rolls which a player does not have permission to see (like blind or whispered rolls) now register a chat message indicating that some dice *were* rolled, but suppressing the result. My thinking is that this change is a positive one for usability and transparency, in addition to more closely resembling the in-person experience, however, I do want to collect feedback on this to understand if any players are negatively impacted by this change for their own games.
- Added a new copy+paste workflow for the Walls layer which allows for groups of Wall objects to be copy+pasted in their current orientation to a new location in the Scene. This can be particularly helpful if setting up walls for many similarly shaped objects like trees or pillars.
- Entities and Folders are now able to be manually sorted through an integer sort key. To re-arrange folders or entities simply drag and drop them on each other. The new position of the Entity or Folder will be placed after the sibling that it is dropped on. You can also drag and rearrange the folder structure, changing parent folders to subfolders, moving subfolders to a new parent, and more. These organizational changes have been long awaited and I hope the community enjoys the new freedom this gives you to organize your content exactly how you wish.
- In addition to manually reordering Entities and Folders within each Sidebar Directory, you may now manually change the order of Scenes in the Scene Navigation menu by drag+drop.
- In addition to manually reordering Entites and Folders, API methods have been added to support manual reordering for Owned Items within a parent Actor. Support for this feature has been incorporated within the D&D5e sheet, but other game systems may need to adopt this API themselves for existing Actor sheets.
- When dragging and dropping to import an Entity from a Compendium pack, the created Entity will go directly into the target expanded Sidebar folder instead of always ending up in the root level of the sidebar directory.
- Removed the anvil watermark image from the World join screen if a custom background image is used.
- Added localization support for many applications including Player Configuration and the new Roll Table Configuration sheet.
- Improved upon the initial dimensions for Token artwork for Tokens with an asymmetric grid footprint (i.e. width != height).
- Improved rendering of all ContextMenu objects to scroll vertically from the origin container if the size of the context menu would cause its content to flow past the lower edge of the window.

### Core Bug Fixes

- Fixed a bug which could sometimes cause a Token health bar not to properly re-render when the underlying attribute data was changed for certain actor edge cases.
- Corrected a problem with version checking where the `isNewerVersion(v1, v0)` helper method was not correctly recognizing updates to a major or minor version as indicating a newer semantic version string.
- Fixed a problem with group Wall editing now that the updateMany method is used which caused trouble once the Walls Layer was refreshed after an update.
- Resolved a problem with repeated EULA license acknowledgement prompts due to an incorrect relative path for Electron application builds. After this update, you should only be prompted to accept the EULA once (initially) and then again only if the terms are changed.
- Fixed a bug with light sources not being correctly masked by their FOV polygons. This resulted from an incorrect Linux build which failed to include updates to the PIXI library as intended.
- Resolved an edge case issue that could cause the Combat Tracker reset all button not to function properly and re-render the tracker for connected clients.
- Corrected a regression which caused tokens with zero vision distance to instead be treated as if they do not have vision enabled. Now Tokens with zero vision receive only a minimal radius of dim vision to allow the player to see their own token but nothing else.
- Solved an issue with syntax errors in the Chat Log export workflow.
- Fixed a problem with the "Delete All" workflow for Folders (and their contained entities) which incorrectly left the contained entities displayed within the Sidebar Directory.
- Fixed an i18n problem with the Player Config window missing many labels.
- Prevented an exception which was being raised when clicking on tab icons of a collapsed Sidebar.
- The Scene Navigation bar was incorrectly blocking mouse pointer events when collapsed. This no longer occurs.
- Added some additional onUpdate steps which must occur if the current User's permission level changes during a game session.
- Correct a translation gap where some strings for the Combat Tracker were not localized correctly.
- Replaced incorrect usage of the ruler icon for multiple sections of the Scene configuration sheet.
- Fixed an issue which caused limited light angle tokens to not work as expected if their visible angle was greater than 180 degrees.
- Applied a better _onUpdate behavior for tokens which will conceal any active Token HUD if the Token is moved to some new position by a different user.
- Capture any errors which may occur during chat log rendering to avoid having a single defective chat message break rendering for the remainder of the log.
- Capture any errors which may occur during the rendering of a Sidebar Tab to avoid having any single defective tab break rendering for the remainder of the Sidebar.
- Capture any errors which may occur during the execution of a user-registered Hook function to prevent potentially erroneous module code from breaking the main FVTT execution.
- Corrected a problem which, when launching the application with a specific `--world flag` - you would not have an opportunity to accept the EULA if a license agreement is needed. Now, if the EULA needs to be signed, the `--world` flag will not function and you must start the application normally.
- Resolved another way that World-level compendium packs could get created incorrectly with an absolute path instead of a relative one. I realize this issue keeps popping up, so I appreciate your patience with the several failed attempts to fix this problem. I am hopeful that this round of correction will knock it out for good, but if not I will keep working to solve it.

### Core Software, APIs, and Module Development

- I have comprehensively (I think) standardized the signature of SocketInterface trigger and triggerMany operations to adopt the same signature in all cases. See https://gitlab.com/foundrynet/foundryvtt/issues/1544 for an example. There were many small changes as part of this improvement including an improved SocketInterface.trigger API, better logging for pre-Hook prevention, and server-side refactoring to a more standardized handling workflow.
- The global configuration variables which was previously in the constants file have been refactored to all exist as children of the `CONST` global object. For temporary backwards-compatibility global references to these variables have been preserved, but this support will be removed before launch. If you were previously using a global configuration parameter (note, I am not talking about the `CONFIG` object) you should migrate to reference it through the `CONST` namespace instead.
- Introduce a new `updateManyOwnedItem` helper method for the Actor class to simultaneously update many Items which belong to a parent Actor entity.
- Improved the behavior of the `diffObject` helper. Previously if one object in a comparison was empty while the other was not, it would report that the new object was not different from the previous. For example `diffObject({foo: {bar: 1}}, {foo: {}}); // {}`. Now this comparison will report that the new object is empty.
- Improved the behavior of the `flattenObject` helper. Previously if the expanded object contains a key which, itself, contains an empty object, the inner empty object would be lost in the flattening process. Now contained objects which are empty are preserved as the final keys of a flattened object. For example `flattenObject({foo: {bar: {}}}) // {"foo.bar": {}}`
- Replaced usages of `Number.prototype.between(min, max)` with a new static helper `Number.between(num, min, max)` which avoids unecessary conversion of primitive `number` type data and improves performance both in terms of execution time and memory utilization. This small improvement can have significant benefits for lighting and vision rendering time. Thanks to tposney for sharing an insight which was helpful in identifying the need for this change.
- The `source` attribute of the `Collection` class has been changed to be private, effective immediately. Module developers should avoid referencing this data and should instead always reference the constructed entities array.
- Retired the specialized `activateScene` socket operation for triggering Scene activation. After investments in the overall hooks system, there is enough data granularity to identify that a Scene has been activated through the traditional `updateScene` socket, so all usages of the old activation approach have been replaced with a straightforward Scene update call which sets the active state directly.
- Incorporate specialized Electron handling for SSL certificates to allow the certificate to be valid for localhost addresses.
- Added a debugging setting which displays logging information to the console every time a Hook function is called. This makes it easier to discover what hooks (and what are their arguments) are applied when conducting workflows in the VTT. To enable this level of debugging, set `CONFIG.debug.hooks = true;`.
- The `Compendium.importEntity` method now accepts an optional argument for `updateData` which allows for conveniently updating the entity simultaneously with the import operation. This can be helpful if you want to programmatically import an entity from a compendium pack, but modify the imported entity relative to it's stock variant.
- Added a `Folder.entities` getter for convenience to vend an Array of all Entity instances which belong to that parent Folder.
- Added some additional fields for package metadata to the conventional NPM package.json file.
- Applied a stronger server-side permission check for Entity updates to validate that the requesting User has ownership permission over the specific document in question.
- The underlying data structure for the buttons in the SceneControls app has been refactored from an Object (prior) to an Array (new). This has several advantages, including allowing for the order and composition of buttons to be manipulated by a new Hook which has been added. By hooking to `getSceneControlButtons` module authors may itroduce new buttons to the controls menu or modify the behavior of existing buttons. Please see https://gitlab.com/foundrynet/foundryvtt/issues/1528 for discussion and examples.
- Improved the protection against cases where folders exceed the maximum allowed level of depth. Previously this would cause the entire Sidebar Tab to fail rendering. Now folders which exist at an invalid depth level are simply rendered at the root level of the sidebar directory.
- Re-wrote and greatly improved the ChatMessage.getSpeaker() helper to construct the `speaker` data object from a given Token, Actor, or User entity.
- Provided a new `canvasPan` Hook event to respond to changes to the canvas location or scale. This hook will fire whenever the canvas is panned (which can result in a lot of calls). Be careful if you use this hook to make sure your hooked function is as efficient as possible. See https://gitlab.com/foundrynet/foundryvtt/issues/1500 for more details.
- Each registered Hook function is now assigned a numeric ID which can now be used as a token for unregistering (turning off) the Hook instead of the hooked function reference. This makes it much easier to un-register a Hook while still using anonymous functions. See https://gitlab.com/foundrynet/foundryvtt/issues/1490 for an example.
- Instaces of the `ImagePopout` class may not optionally refer back to an Entity instance which requested them to be shown. If such an entity reference exists, it is available under `options.entity` of the ImagePopout instance.
- Added a simple CLI script which can quickly initialize a new module, creating some boilerplate structure for module developers to quickly build upon. See https://gitlab.com/foundrynet/foundryvtt/issues/1374 for example usage.

### D&D5e System Improvements

- Owned Items may now be manually reordered through drag+drop within the D&D5e character and NPC sheets.
- Renamed the "Feats" tab on character sheets to "Features" to more appropriately reflect it's intended use case as the location for both Feats as well as class, racial, or background Features.
- A number of bug fixes and minor improvements for the D&D5e system to keep up with core VTT changes.

## Beta Version 0.3.8, 2019-10-05

Dear Patreon supporters, I am back from my vacation which was very relaxing - and I've been diving back into an exciting new set of features for Foundry Virtual Tabletop Beta update 0.3.8. The two most significant updates in this version include angle-restriction vision and light emission which allows Tokens and Ambient Light sources to limit their field of effect to some frontal-angle. Additionally improved options for Map Notes allows for users to organize better by customizing icon size, color, and labeling preferences while associating journal entries with various Scenes.

Thank you all for appreciating my work, providing thoughtful feedback, and encouraging me to do even more. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### New Features

- Support limited vision and light emission angles for Token and AmbientLight objects. This allows the visibility or light emitted by an object to be restricted to a certain frontal angle relative to the object's direction of facing. The performance impacts of using limited angles are mixed - for light sources, restricting the angle of emission is actually somewhat beneficial for performance as it results in fewer rays being cast and fewer collision tests against walls. For Tokens, there is a benefit due to fewer rays, but also an additional cost because fog of war exploration caching is less efficient. Please experiment with this new feature and share any observations you have about how it's performance compares to what you observe for unrestricted Tokens or light sources.
- The Scene Navigation menu has received some styling improvements and may now be collapsed or expanded using a small toggle button on the left side.
- Added internationalization string translations for the Navigation Menu and its context options.
- The preference for whether to toggle the display of Map Notes on the Token Layer is now saved as a client-side setting that will persist across sessions.
- Allow Map Notes to have additional stylistic customization for icon size, font size, icon tint, and text anchor point.
- Map Notes may now override the text title which is displayed. The default label is still the title of the associated Journal Entry, but this can be overridden to reveal different information in the tooltip.
- Improve the saving behavior of Journal Entries which will now automatically save any changes before the entry is closed, it's display mode is swapped, or it is shown to other users.
- Begin with Playlist entities in the sidebar directory initially in a collapsed state and switch to record which are, instead, expanded.
- Imposed a rate limit on PlaceableObject rotation operations to restrict rotation to 1 update per 100ms. This rate limit is especially important for mice or other hardware which feature continuous scrolling - where such hardware was previously generating hundreds of database update operations per second.
- Substantially improved the generality and performance of multi-object update operations within Scenes. This better allows for many objects to be updated simultaneously with less costly database updates and more efficient canvas refresh.
- Now that Wall objects are controllable (either via individual or chain selection) - Walls can no longer be deleted only by hovering over them while pressing the delete key. This reduces the chance that users will accidentally delete the incorrect wall while navigating the Walls layer.
- Changed the Settings tab sidebar icon from a question mark to cogs.
- It is no longer possible to delete a Tile or Drawing which has been locked. You must first unlock the object before it can be deleted.
- Localization support has been added for many applications including the sidebar and all its tabs, the Setup configuration sheet, Player configuration, Scene Navigation, and more. Thanks to Ayan for helping with this process by sharing a set of localized templates.
- The **End User License Agreement** has been updated to Beta Version 0.3.8. It now includes a clause which expressly disallows temporarily renting access to the software.
- Non-GM users are now able to undo changes to their own controlled objects. Previously only game-masters had permission to undo changes. After this change, GM users may undo changes made by any player, while non-GM users may undo their own changes.
- Multiple object operations supported by the new updateMany and deleteMany events are now tracked as part of layer history, which allows them to be un-done in the case of an accident. Things like deleting all objects from a layer can now be recovered via CTRL+Z.
- Worlds may now be configured to feature a custom background image which will be used to greet players which connect to the server on the /join screen.
- Improved the set of default icons which are available for Token status effects tracking to feature icons which are more useful for several very common conditions like prone, blind, deaf, or asleep. Additionally added several new location icons as options for Journal Notes. This icon set will continue to be expanded and improved over time.

### Core Bug Fixes

- Resolved a permission issue which incorrectly allowed players to configure a Map Note via right-click.
- Attempt (again) to resolve possible non-determinism in combatant sorting order.
- Solved two bugs for vision and fog of war which could allow a small slit of visibility to be incorrectly allowed between Wall endpoints under two circumstances. One where the angles of ray emission fell subject to floating point precision issues and a second where a Terrain wall endpoint intersected with a non-terrain Wall.
- Fixed a bug with the server-side Entity update process which accidentally discarded additional context options from the request.
- Fixed a bug with blind roll chat parsing which prevented the `/br`, `/broll`, or `/blindroll` commands from functioning.
- Fix a problem with the SceneControls application which caused the underlying data to be mutated during it's render operation.
- Improved the behavior of deleting multiple objects to ensure that the controlled objects array is cleared for the parent layer.
- I have attempted a solution for a problem which causes the Fog of War polygon to shift slightly each time the fog render layer is swapped to disk. I am unsure whether the fix I have applied will solve all use cases - but in my own local testing I was able to eliminate the problem. I am hopeful to hear feedback from the community if anyone experiences this issue before or after the update.
- Corrected a problem with Chat Bubbles which caused them to not trigger correctly for certain chat message types.
- Corrected inconsistent form styling for the Combat Tracker config where hints were shown above the option, instead of below.
- Solved a problem which could prevent the Sight Layer from correctly refreshing when a Token's vision was disabled.
- Fixed an issue with Ambient Sound easing which caused it's volume to not respect the main volume slider for the sound. The volume slider for AmbientSounds now represents the maximum volume for the sound, as heard when an observer is immediately on top of it's origin.
- Default chat speaker identification now prioritizes a controlled token over a non-controlled token which represents the player's impersonated actor.
- Resolved a problem which could cause World-level compendium packs to be written to the world.json file with absolute paths instead of relative ones.
- Fixed a bug for Firefox which prevented newly created Worlds from properly receiving their server-side response, resulting in a hanging page load.
- Corrected a problem where elements in the Settings template did not correctly assign a `data-dtype` attribute.
- Fixed a problem with the Token HUD which prevented some values of an incremental attribute bar update from having the correct effect due to leading spaces or an incorrect string type conversion.

### Core Software, APIs, and Module Development

- Addressed three security vulnerabilities in the server-side application. Thanks to Azzurite for pointing out several weak points.
- Added a dedicated `updateMany` function and socket logic for every PlaceableObjects layer. See the [GitLab issue](https://gitlab.com/foundrynet/foundryvtt/issues/1462) for more details and example usage.
- Added a dedicated `deleteMany` function and socket logic for every PlaceableObjects layer. See the [GitLab issue](https://gitlab.com/foundrynet/foundryvtt/issues/1466) for more details and example usage.
- Developed a generalized framework for handling the initialization of audio and video playback following an observed user interaction. This framework is now applied for all audio and video playback requests within the PIXI canvas to ensure that web autoplay standards are followed for modern browsers. This change should hopefully fix problems in previous versions with video map backgrounds or tiles.
- Implemented an optimization for dynamic vision polygon generation which can realize performance improvements for large maps which have many small wall segments.
- Added a Hook which allows for modules to insert additional context menu options for Scenes in the top navigation menu using `Hooks.on("getSceneNavigationContext", (html, menuOptions) => ());`.
- Added a Hook which allows modules to respond to the Scene Navigation application being expanded or collapsed using `Hooks.on("collapseSceneNavigation", collapsed => ());`.
- Added helper methods for `setFlag()` and `getFlag()` attached to all PlaceableObject instances with the same signature as those offered by the `Entity` class.
- Removed the linked Journal Entry as a required field of the Map Note data model, it is still recommended to create notes which reference Journal Entries, but this is not required. There is no UI-based method for doing this, but programmatic Note creation will function without an `entryId` attribute.
- Provide an improved `ChatMessage.alias` getter to centralize the logic for determining the recommended display name for the author of a chat message.
- Added a PlaceablesLayer.rotateMany method which can be used to control rotation of multiple PlaceableObject instances with a single database operation.
- Refactor the server-side Entity socket responses to explicitly separate the options Object from the primary response subject. This is a backend change which does not impact users of the standard API methods. These additional options are now passed as an additional argument to create, update, and delete hooks for various entities. For example, `Hooks.on("createActor", (actor, options) => {});`.
- The `Token.moveMany` and `Tile.moveMany` methods have been **deprecated**, effective immediately, in favor of a generalized `PlaceablesLayer.moveMany` method with a revised signature. If you were using the previous Token.moveMany method you must migrate immediately to the new approach.
- No longer require the coordiantes of Drawing objects to be integers, as this was causing polygons and freehand to become distorted when resized to a small size.
- Changed the behavior of the `PlaceablesLayer.copyObjects` function to store references to the copied objects themselves instead of just their data - this can give downstream APIs access to the full context of the origin objects, including the Scene from which they originate.
- Added a Hook event to allow developers to respond when multiple PlaceableObjects are pasted onto a canvas layer. See the [GitLab issue](https://gitlab.com/foundrynet/foundryvtt/issues/1483) for more details.
- Added several attributes to `ui.sidebar` to facilitiate module development including `activeTab` and `popouts`.
- An issue with the Chat Log template caused it to be incorrectly injected into another sidebar tab when manually re-rendered. This no longer occurs.
- Added a `filterObject(object, keys)` core helper function which reduces an object to a subset of its keys by name, returning the filtered object.
- The requesting User ID is now included as an optional final argument in CRUD socket event handlers.
- Redesigned the order in which page requests are handled by the Express server to resolve explicitly named view paths first before serving any unhandled requests as static files.

### D&D5e System Improvements

- Game-ready Actor entries have been added for all CR 1/2 monsters in the SRD Monsters compendium pack.
- Incorporated wonderful token artwork for six CR 1/4 monsters as part of the SRD Monsters compendium. Many thanks to Stryxin from Forgotten Adventures for his support of this project and permission to include his wonderful tokens.
- Improve the SRD Spells compendium by adding Tiny Hut, Secret Chest, Freezing Sphere, and Telepathic Bond while removing Telepathy which is not covered under the OGL.
- Removed a superfluous Promise chain from the rollToolCheck function in the Item5e class.
- Allow inventory items on a character sheet to have a quantity of zero, for cases where the player wishes to track a placeholder item even if none of that item is owned.
- Fix a bug which caused global save modifiers to be double-counted when saving throws were rolled through the sheet dialog.
- Added an optional setting to disable experience tracking for player characters. Thanks to bensku for submitting a merge request with this feature.

## Beta Version 0.3.7, 2019-09-14

Hi everyone. This update is a bit less conventional - I am releasing a small update focused on some bug fixes for various known issues which emerged since 0.3.6. I am releasing these changes promptly because I will be taking a much needed vacation for the next two weeks!

During that time I will be working (a little bit) on some new VTT features, but I didn't want to hold up these bug fixes until after my travel since they can correct a couple of small problems which currently affect players. During vacation, I will be in touch periodically with the community through normal channels, although expect me to be less active on Discord than usual until I return at the end of the month.

Thank you all for the continued support for the project and your contributions towards growing the awesome Foundry community. As always, please keep an eye on the development progress board here for visibility into what features are in progress and coming up next!

[https://gitlab.com/foundrynet/foundryvtt/boards](https://gitlab.com/foundrynet/foundryvtt/boards)

### Core Bug Fixes

- Corrected a regression where the default chat message type was no longer in character in cases where a Token was selected.
- Resolved a problem which prevented the Chat Log from being exportable when a dice roll was present in the chat history.
- Fixed an issue which failed to apply the correct in-character or emote chat stylings to chat bubbles and messages after the 0.3.6 changes.
- Corrected a limitation which prevented a GM user from dragging a Map Note in cases where the default note permission level was set to LIMITED.
- Solved a problem which prevented Entities from being imported from JSON, instead simply displaying the export prompt.
- Improved the process of World editing through the configuration sheet on the setup menu, correctly populating the current World path and fixing issues with MCE editor saving.
- Corrected some mis-translated strings in the Scene Config application.
- Fix an issue which impacts compendium migration for Entity types which do not define a data model in their system template.

### Core Software, APIs, and Module Development

- Moved the "Worlds" tab to be in the first (left-most) position of the setup view.
- Define a default ChatMessage type as "OTHER" to correct breakages to existing ChatMessage.create calls, however it is strongly recommended for system and module developers to pass an explicit type from the CHAT_MESSAGE_TYPES object at the point of message creation.

### D&D5e System Improvements

- Corrected a problem with the Damage dialog prompt for rolling Critical damage which raised a roll error.

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
- You may now include some additional flavor text along with any dice roll submitted in the chat window by separating the roll portion of the command with a `#` character. For example `/roll 4d6kh # Rolling for ability scores`!.
- Added additional buttons to the Settings sidebar as an alternative way to return to key setup menu screens. There are new buttons for "Return to Setup", "Configure Players", and "Log Out".
- Added a new button on the Settings tab of the sidebar to render the Community Wiki documentation in a pop-out iframe. Many thanks to errational, CyberPathogen, and the many other wonderful curators and contributors of the community wiki for creating this helpful resource.
- The ability to export-to-JSON and import-from-JSON has been added for more Entity types - including Items, Journal Entries, and Scenes. Previously only Actors had this capability.
- Added localization support for context-menu options on Sidebar Directory containers.
- Added a new Journal Entry context menu option to Duplicate an existing entry, as was possible for other Entity types.
- Improve the hit area definition of newly added Drawings from the 0.3.5 update so they are easier to select and manipulate once drawn.
- Made a change which allows chat commands to span multiple lines without being incorrectly truncated.
- Users who have "Limited" permission to a Journal Entry will now be able to see Map Notes placed for that entry, but will not be able to inspect the details of the note. This can allow GMs an alternative option for label significant locations without revealing details about those locations to players or needing to keep those details in a separate entry.
- A User's chosen color is now shown as a border around all out of character chat messages sent by that User.
- The syntax for sending whispered messages in chat has been made more flexible to support `/w` and `/whisper` prefixes in addition to the previous @User syntax.
- Web URLs posted in chat messages will be automatically converted to a clickable hyperlink.

### Core Bug Fixes

- Fixed an issue with attempting to add an Owned Item directly to an Item type compendium.
- Changing the Actor that a Token references would not fully take effect until a hard refresh, as double-clicking the Token would continue to open the old Actor's sheet.
- Fixed a problem with IP address identification which sometimes resulted in the local and internet IPs not being properly displayed.
- Solved a problem for newly created Actors which prevented the `img` attribute from being initially present in their prototype Token data model.
- Hardened a loophole with EULA acceptance which previously allowed you to simply close the window to dismiss the agreement without later prompting.
- Applied a fix for the PIXI v5 update which caused a vertex buffer overflow when rendering large Graphics objects (like big Hex grids). This caused hexagonal grids to no longer render after some number of polygons.
- Fixed a problem that occured when deleting a World-level compendium pack which had not yet connected to its database.
- Removed visibility of the "Delete All" button on the Measured Templates layer for players who could not use that button as they lack GM permission.
- Made a change to lock tiles while they are in the middle of a drag workflow. Previously the Tile could be rotated via mousewheel while mid-drag causing server desynchronization problems.
- Applied an additional check to prevent Compendium pack paths from being written to world files as absolute paths instead of relative to the World directory as intented.
- Fixed an issue since the PIXI v5 migration which prevented Scene background color from being properly applied.
- Corrected the rendering of large hex grids in 0.3.5 which produced an incorrect offset with artifact lines.
- Improve the vertical spacing of TinyMCE editors since the v4.x update in 0.3.5 to make better use of the bounding container.
- Fixed an order-of-operations problem with the `unregisterSheet` method which caused it to incorrectly clear a previously registered sheet for all Entity types, even if a specific type of entity to no longer use the sheet for was specified.
- Improved the logic of the version comparison function used to detect module and system update availability to work for more types of versioning schema.
- Fixed a bug in the "Simple Worldbuilding" system which prevented Owned Items from being properly editable.
- An unintentional "feature" in 0.3.5 caused mousing over a Polygon point during a drawing creation workflow to undo that point. This, while sometimes nice, was an unintentional workflow that could sometimes produce frustrating results and has been removed.
- Fixed a bug whereby an Owned Item could be dropped on the Actor who owns it, thereby duplicating the item data in that Actor.
- Drawing objects can no longer have no line, no fill, and no text - causing them to become effectively invisible. Drawings must have at least one of these values set.
- Remove the "Delete All" button from Players on the Drawing layer since they do not have GM permission to delete the drawings of others. This was a bug fix for now, but I may bring this back in the future where the button would only delete drawings belonging to the user.
- Corrected accidental residual references to `CONFIG.Token` which has been removed in favor of other global configurations.
- Improved the approach towards regex matching for chat message whispers and dynamic entity links to better support international characters in Firefox where unicode regex escapes are not supported.

### Core Software, APIs, and Module Development

- The server-side implementations of "Pakcages": System, Module, and World have all been jointly refactored to extend the same abstract base Package interface and share much more common code and implementation. This has improved quality and consistency of how these packages are managed and described within the VTT software.
- Broadly refactored and improved code quality for the Chat Log sidebar and the messages that are rendered within it. This was some of the oldest FVTT code, as chat was one of the first features I implemented. It was well overdue for a fresh coat of paint.
- Refactored the sidebar directory templates and CSS rules to adopt a flexbox layout which should be more friendly for mod developers who want to add additional content into the sidebar.
- The `ChatMessage` Entity now has a required `type` field added to its data model to more explicitly differentiate different types of chat communication. The valid types of chat messages are enumerated in `CHAT_MESSAGE_TYPES`.
- Some changes to keystroke handling have been implemented. Several keys were previously only captured on keyup, which are now captured on keydown with a repetition filter added. This provides a more responsive experience when interacting with these controls.
- Performed some code cleanup in the Combat class to remove some deprecated properties and bring greater consistency to the structure for current and previous round tracking.
- Improved the informativeness of the error message thrown if the `--world` startup flag references a World which does not exist.
- An informative fatal error is now triggered if there are multiple packages (systems, modules, worlds) which have the same "name" attribute in their manifest files.
- A new structure is supported (and enforced) for defining module-based translation files. Under this new approach, languages are defined as an Array of Objects, and JavaScript code is no longer required to manipulate the CONFIG object as this is handled automatically. See this [issue on GitLab](https://gitlab.com/foundrynet/foundryvtt/issues/1342) for more details.
- English language translations are now always used as a fallback option for any localization strings which do not have an available translation in the designated preferred locale.
- Because of the new management strategy for module-provided translation files, these translations are now accessible on the main configuration and setup pages of the Application where modules were previously not able to contribute content.
- Improved server-side zip file extraction to support an option to de-dupe the folder structure during the extraction process if nested directories are present.
- Added a `confirmDialog()` helper function to streamline the process of rendering standard yes/no prompts using less code.
- Revisit support for `options.height = "auto"` to be specified in an Application render options - auto height applications will be automatically resized (vertically) when they ar re-rendered to accomodate changes to the internal content.
- Improve server-side Socket management to automatically learn the Entity class names for which to open socket listeners instead of hard-coding them.
- Added a very simple `Number.isNumeric()` helper method to test whether a string represents a numeric value.
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
