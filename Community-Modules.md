<!--tl=2-->
<!--ts-->
   * [Foundry VTT Modules (Universal)](#foundry-vtt-modules-universal)
      * [Always Show Notes](#always-show-notes)
      * [Chat Autoloader](#chat-autoloader)
      * [Combat Ready](#combat-ready)
      * [Deselection](#deselection)
      * [Dice Calculator](#dice-calculator)
      * [Display mode](#display-mode)
      * [Entity Order](#entity-order)
      * [FFG Roller](#ffg-roller)
      * [The Furnace](#the-furnace)
      * [Popout!](#popout)
      * [GM Roll Message](#gm-roll-message)
      * [Grid Scaler](#grid-scaler)
      * [Image Previewer](#image-previewer)
      * [Infinite Folders](#infinite-folders)
      * [Journal Enhancer](#journal-enhancer)
      * [Layer Hotkeys](#layer-hotkeys)
      * [Less Fog](#less-fog)
      * [Message Age Restriction](#message-age-restriction)
      * [No Token Animations](#no-token-animations)
      * [Patches by trdischat](#patches-by-trdischat)
      * [Permission Viewer](#permission-viewer)
      * [Pointer](#pointer)
      * [SVG Loader](#svg-loader)
      * [Tiles Browser](#tiles-browser)
      * [VTTA Tokenizer](#vtta-tokenizer)
      * [Token Mold](#token-mold)
      * [Z Order](#z-order)
   * [Foundry VTT Modules for DnD 5E](#foundry-vtt-modules-for-dnd-5e)
      * [Better NPC Sheet 5e](#better-npc-sheet-5e)
      * [Beyond 20](#beyond-20)
      * [Chat Damage Buttons](#chat-damage-buttons)
      * [Chat Damage Buttons - Better Rolls Edition](#chat-damage-buttons---better-rolls-edition)
      * [DDB Popper](#ddb-popper)
      * [DnD Beyond Character Importer](#dnd-beyond-character-importer)
      * [Favourite Item Tab](#favourite-item-tab)
      * [Group Roll](#group-roll)
      * [Item Sheet Buttons](#item-sheet-buttons)
      * [Loot Sheet NPC (5e)](#loot-sheet-npc-5e)
      * [Minor QOL Improvements](#minor-qol-improvements)
      * [NPC Browser](#npc-browser)
      * [Polymorpher](#polymorpher)
      * [R20 Converter](#r20-converter)
      * [Roll20 NPC Importer, for 5e](#roll20-npc-importer-for-5e)
      * [Sky's 5th Edition Dungeons &amp; Dragons Sheet](#skys-5th-edition-dungeons--dragons-sheet)
      * [Spell Browser](#spell-browser)
      * [SRD Bestiary Module](#srd-bestiary-module)
      * [VTTA Party](#vtta-party)
   * [Foundry VTT Modules for WFRP 4E](#foundry-vtt-modules-for-wfrp-4e)
      * [Arcane Marks &amp; Careers](#arcane-marks--careers)
   * [Foundry VTT Modules (Defunct)](#foundry-vtt-modules-defunct)
      * [aDnD5e](#adnd5e)
      * [Encumbrance Variant](#encumbrance-variant)
      * [FVTT-Party (Discontinued, see VTTA-Party for an successor)](#fvtt-party-discontinued-see-vtta-party-for-an-successor)
   * [Appendix](#appendix)
      * [Appendix A: Adding a Module](#appendix-a-adding-a-module)
      * [Appendix B: Best Editing Practices](#appendix-b-best-editing-practices)
<!--te-->

# Foundry VTT Modules (Universal)

Foundry modules that work across all or most systems are noted here. These may include reskins, general improvement mods, and more.

## Always Show Notes

* **Author**: Pin#8969
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.5
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: N/A
* **Module Conflicts**: No known conflicts
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/Pingar5/alwaysshownotes](https://github.com/Pingar5/alwaysshownotes)

### Description
Sets the Display Notes toggle to true by default

---

## Chat Autoloader

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: 0.1
* **Foundry VTT Compatibility**: At least v0.3.2+, propably earlier versions as well.
* **Module Conflicts**: Possible conflicts with *Message Age Restriction* by Felix@6196.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/chat-autoloader](https://gitlab.com/moerills-fvtt-modules/chat-autoloader)

### Description
This module improves loading times by only rendering the last few chat messages at page load. Older messages will automatically get rendered while scrolling to the top. (This behaviour is similar to e.g. scrolling in Discords chat)

---

## Combat Ready

* **Author**: Ken L. (Ayan)
* **Version**: 1.1
* **Foundry VTT Compatibility**: 0.3.7 +
* **Module Conflicts**: None
* **Translation Support**: EN/JA/KO/FR/BR (full) NL/IT (partial)

### Link(s) to Module
* [https://gitlab.com/Ayanzo/combatready](https://gitlab.com/Ayanzo/combatready)

### Description
Shows a graphic + sound for players a round just before a player's turn (Next Up) and
during their turn.

It uses a light-box style darkening of the canvas to catch their attention as
well as an animated graphic + sound. The player then needs to click the banner to
either acknowledge their turn is coming up, or take their turn. If they somehow
still don't know its their turn then that's a problem between chair and keyboard.

Note that for "Next UP" rather than having the graphic go away entirely, it just
puts opacity on the banner as a constant reminder for the player to plan for
their turn for when it does come up. Works with hidden combatants too, such that
even if there's a block of hidden enemies you're working on as GM, they'll know
when their turn is 'next' due to the graphic as to not catch them by surprise.

The combat timer is simply a bar along the bottom of the screen. By default it is
configured for 3m, but this can be changed in the settings. When the bar
reaches 3m, or the custom value, an 'expired' sound will play, but it does not
automatically advance the turn. Shame is good enough in my opinion. If you need
to pause the timer, it responds to FVTT's pause mechanic.

---

## Deselection

* **Author**: Sky#9435, KaKaRoTo#4756 (Discord). KaKaRoTo's Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto).
* **Version**: 1.0
* **Foundry VTT Compatibility**: 0.3.4+
* **System Compatibility**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/Sky-Captain-13/foundry/tree/master/deselection](https://github.com/Sky-Captain-13/foundry/tree/master/deselection)

### Description
This module lets the GM deselect a token or tokens by clicking anywhere on the map.

---

## Dice Calculator

* **Author**: Asacolips#1867 on Discord.
* **Version**: 0.3.0
* **Foundry VTT Compatibility**: 0.3.0+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/asacolips-projects/foundry-mods/foundry-vtt-dice-calculator](https://gitlab.com/asacolips-projects/foundry-mods/foundry-vtt-dice-calculator)

### Description
This module turns the d20 icon near the chat prompt into a clickable link that opens up a new dice calculator dialog. The dice calculator includes buttons for dice, numbers, and simple math. [Screenshot of the calculator can be found here.](https://i.imgur.com/ar2hNYP.png)

---

## Display mode

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de
* **Version**: 0.1
* **Foundry VTT Compatibility**: At least 0.3.0+, and will likely work with previous versions.
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/displaymode](https://github.com/syl3r86/displaymode) 

### Description
This module makes it so that when you click the anvil in the top left of the screen, the sidebar in Foundry is hidden.

---

## Entity Order

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.1+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-entityorder](https://github.com/kakaroto/fvtt-module-entityorder) 

### Description
This Foundry VTT module allows you to re-order entities (Actors, Scenes, Items and Journal entries).

---

## FFG Roller

* **Author**: Petep, @petep#0441 on Discord
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal, but you'll want to probably use it with the simple system
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/petepeg/FFG-Roller](https://github.com/petepeg/FFG-Roller)

### Description
This adds a simple dice rolling window for the special dice used in Fantasy Flight Games Star Wars RPG and Genesys. 

---

## The Furnace

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 1.0
* **Foundry VTT Compatibility**: 0.3.5+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-furnace](https://github.com/kakaroto/fvtt-module-furnace) 

### Description
The Furnace is an essential part of every Foundry. This Foundry VTT module brings Quality of Life Improvements to the VTT.

It started by adding Drawing Tools, and then an experimental Macros system and now it also adds a 'Split Journal' feature. More QoL improvements are planned.

---

## Popout!

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-popout](https://github.com/kakaroto/fvtt-module-popout) 

### Description
This Foundry VTT module lets you pop out journal entries into their own windows. It is currently acting as a proof of concept.

---

## GM Roll Message

* **Author**: Hydroxi#0366 on Discord.
* **Version**: WIP
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/Hydroxi/gmrollmessage](https://github.com/Hydroxi/gmrollmessage) 

### Description
Sends an extra public message/hint when rolling a `gmroll` or `blindroll`.

---

## Grid Scaler

* **Author**: UberV, UberV#2154 on Discord.
* **Version**: 0.0.5
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/UberV/scaleGrid/](https://github.com/UberV/scaleGrid/) 

### Description
This mod allows you to resize a grid more easily within Foundry, allowing easier map setup when a grid is uneven or unclear within a background image.

---

## Image Previewer

* **Author**: Felix#6196 on Discord, accepts donations via paypal, felix.mueller.86@web.de
* **Version**: 0.1
* **Foundry VTT Compatibility**: written for 0.3.4, should be fairly version independant
* **System Compatibility (If applicable)**: universal
* **Module Requirement(s)**: none
* **Module Conflicts**: none
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/image-previewer](https://github.com/syl3r86/image-previewer)

### Description
A little app to preview images on hover in the file picker menu.
#### Installation
1. Download the [image-previewer.zip](https://github.com/syl3r86/image-previewer/raw/master/image-previewer.zip)
2. Unzip it into FoundryVTT/resources/app/public/modules
3. Restart Foundry if it was running.
4. Enable the module in the Module Configuration

---

## Infinite Folders

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.1
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: This module creates folders and allows you to create data where it shouldn't be. If a future FVTT update enforces the 2-depth limit on the server side, then all of the deeper folders and their content may be lost.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-infinite-folders](https://github.com/kakaroto/fvtt-module-infinite-folders) 

### Description
This Foundry VTT module allows you to create infinite depth of folders for Scenes, Actors, Items and Journals. No more limit to a depth of 2 folders (or none for Journal entries). This will also add a `New entity` button on folders so you can create it directly in the folder (does not work for Scenes though).

---

## Journal Enhancer

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: Version 0.2
* **Foundry VTT Compatibility**: 0.2.10
* **System Compatibility (If applicable)**: As of right now, it is universally applicable to all existing systems.
* **Module Requirement(s)**: None
* **Module Conflicts**: None currently known
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/journal-enhancer](https://gitlab.com/moerills-fvtt-modules/journal-enhancer) 

### Description 
This module adds a search function for journal entries, includes a “jump to pin” button for moving the camera to a pinned journal entry, adds a zoom function for image handouts, and hides the name of a handout to users without permissions set. Moerill includes a video showing off the mod’s utility here: [https://youtu.be/5O4yA8Kr6bs](https://youtu.be/5O4yA8Kr6bs)

---

## Layer Hotkeys

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: v1.0
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/layer-hotkeys](https://gitlab.com/moerills-fvtt-modules/layer-hotkeys) 

### Description
This module adds hotkeys for switching layers and the active tool in canvas.

Hotkeys are:
- Token Layer : `T` 
- Template/Measurement Layer: `M` 
- Tiles Layer: `I` 
- Walls Layer: `W` 
- Lighting Layer: `L` 
- Sound Layer: `S` 
- Notes Layer: `N` 

The layer tools are accessible through the digits 1 to 9, counted from the first at the top down to the bottom.

The Hotkeys can be seen by hovering over the button as well.

**Quick note**: To see the changed wall-type reflected you need to move the mouse a bit after switching the tool to trigger a color update.

---

## Less Fog

* **Author**: trdischat#2123 on Discord.
* **Version**: 0.0
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal.
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/trdischat/lessfog](https://github.com/trdischat/lessfog) 

### Description
Module to enhance visibility for the GM in Foundry VTT.

---

## Message Age Restriction

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de 
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.1+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/messageagerestriction](https://github.com/syl3r86/messageagerestriction) 

### Description
A Foundry VTT Module to enable filtering chat-messages by their age. Each user can choose his own settings. It is possible to set the maximum age (in days) and to specify if the filter should be applied.

---

## No Token Animations
* **Author**: [Fyorl#1292](https://kim.mantas.me.uk)
* **Version**: 1.0
* **Foundry VTT Compatibility**: 0.3.5+
* **Translation Support**: EN (full)

### Link to Module
* [https://bitbucket.org/Fyorl/notokenanim](https://bitbucket.org/Fyorl/notokenanim)

### Description
Adds an option to the settings dialog to disable token movement animations. Tokens will drop immediately instead of sliding when dragged and dropped around the map with this setting enabled.

---

## Patches by trdischat

* **Author**: trdischat#2123 on Discord.
* **Version**: 0.0
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal.
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/trdischat/fvtt/tree/master/patches](https://github.com/trdischat/fvtt/tree/master/patches) 

### Description
Module to apply the following patches to Foundry VTT:
- `patchFog`: Allow GM to see through the FOW and to see all tokens on the canvas.
- `patchSound`: Apply volume easing to selected volume level of sound effect.
- `patchDice`: Average of 2d20 rolls for normal checks and saves; limit dice to reroll (applies to the dnd5e system).

All patches rely on the `patchClass` utility function.

---

## Permission Viewer

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-permission-viewer](https://github.com/kakaroto/fvtt-module-permission-viewer) 

### Description
This Foundry VTT module displays colored diamonds/squares/circles to represent the players who have limited/observer/owner permissions on Entities (Actors, Journal entries, Items, etc..)

---

## Pointer

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: 1.3
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/pointer](https://gitlab.com/moerills-fvtt-modules/pointer)

### Description
This module adds the ability for each user to show a cursor following his mouse as well as adding the option to ping a certain location.

---

## SVG Loader

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: 
* **Foundry VTT Compatibility**: 
* **System Compatibility (If applicable)**: 
* **Module Requirement(s)**: 
* **Module Conflicts**: 
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/svg-loader](https://gitlab.com/moerills-fvtt-modules/svg-loader) 

### Description
This module allows to load walls, lights and sources through .svg files, provided e.g. by DungeonFog.

---

## Tiles Browser

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.3.5
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/tiles-browser/](https://gitlab.com/moerills-fvtt-modules/tiles-browser/)

### Description
Adds a browser to the tiles layer to conveniently preview and then drag and drop tiles onto the scene. Providing additional features to manipulate tile rotation and size while dragging.

---

## VTTA Tokenizer

* **Author**: solfolango77#0880 on Discord. His Patreon can be found here: [https://www.patreon.com/vttassets](https://www.patreon.com/vttassets) 
* **Version**: v1.0.2-rc.1
* **Foundry VTT Compatibility**: 0.3.5+
* **System Compatibility (If applicable)**:
* **Module Requirement(s)**: Requires the player permission "Trusted Player"
* **Module Conflicts**:
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://www.vttassets.com/asset/vtta-tokenizer](https://www.vttassets.com/asset/vtta-tokenizer)

### Description
Tokenizer provides the user with:
- ability to define a custom token size, defaulting to 400x400 pixels
- the ability to create multiple layers consisting of individual loaded image
- the ability to load images from a) local disk b) a web URL c) the Foundry VTT server
- the ability to scale and translate each layer individually
- automatic generation of a mask using the marching squares algorithm
- automatic upload of the created tokens to the Foundry VTT server (requires 'Trusted Player' permission level)

---

## Token Mold

* **Author**: Moerill#7205 on Discord. He accepts donations at his [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=FYZ294SP2JBGS&source=url).
* **Version**: 1.0
* **Foundry VTT Compatibility**: 0.3.5
* **System Compatibility (If applicable)**: All, though extra option to roll hp for DnD5e
* **Module Conflicts**: This module replaces the *Token Randomizer*, hence it is not compatible with it.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/token-mold](https://gitlab.com/moerills-fvtt-modules/token-mold) 

### Description
What is a foundry without its molds? This module provides you with a customizable mold for your Tokens.  
On creation each unlinked Token will fit snugly into the pattern of your mold.  
**Features**
- Automatic indexing
- Random adjective prefixes (e.g. angry, calm, bloodthirsty, ...)
- Hit Point rolling by formula (currently dnd5e only)
- Overriding default token template config
- Providing a customizable overlay to quickly  check some stats on Token hover

---

## Z Order

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto) 
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Universal
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/fvtt-module-zorder](https://github.com/kakaroto/fvtt-module-zorder) 

### Description
This Foundry VTT module lets you send tiles to the front or the back of the scene.

---

# Foundry VTT Modules for DnD 5E

Foundry modules that work within Dungeons and Dragons 5th Edition are noted here. These may include NPC compendiums that may be legally shared, world saves, character sheet mods, and much, much more.

## Better NPC Sheet 5e

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de 
* **Version**: Better NPC Sheet v0.4.5
* **Foundry VTT Compatibility**: 0.2.9-0.2.10
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition.
* **Module Requirement(s)**: None
* **Module Conflicts**: If used alongside Moerill’s “adnd5e” module, item descriptions are unable to be expanded in the sheet. This can be fixed by disabling Moerill’s module.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/BetterNPCSheet5e](https://github.com/syl3r86/BetterNPCSheet5e) 

### Description
This module overwrites the default NPC sheet that comes shipped with the dnd5e system and brings it closer to the well known official template. It also includes functionality supporting separation of action categories (legendary actions, actions, reactions, etc.), and features the ability to expand and view the description of the ability/action in-sheet.

---

## Beyond 20

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto)
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: This module requires a concurrent browser plugin in either Firefox or Google Chrome.
* **Module Conflicts**: None known
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/kakaroto/Beyond20/](https://github.com/kakaroto/Beyond20/) 

The module is available under the 'FVTT-module' directory.

### Description
This module allows you to use and roll sheets in DnD Beyond, and have those results displayed in Foundry VTT. For more details, see Kakaroto’s module page and readme files.

---

## Chat Damage Buttons

* **Author**: hooking#0492 on Discord.
* **Version**: 0.3.1
* **Foundry VTT Compatibility**: 0.2.8-0.2.10
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s): None.
* **Module Conflicts**: Module appears to be incompatible with the aDnD5e module.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/hooking/foundry-vtt---chat-damage-buttons](https://gitlab.com/hooking/foundry-vtt---chat-damage-buttons) 

### Description
This module replaces the right-click context menu with buttons on the dice-roll chat message. This allows for quicker application of damage/healing.

To install the module, download the zip file included in the Github module directory. Extract the zip file to `/public/modules`. Restart Foundry Virtual Tabletop.

---

## Chat Damage Buttons - Better Rolls Edition

* **Author**: Felix#6196 and hooking#0492
* **Version**: 0.1
* **Foundry VTT Compatibility**: written for and tested on v0.3.6
* **Module Requirement(s)**: [Better Rolls for 5e](https://github.com/RedReign/FoundryVTT-BetterRolls5e) by RedReign
* **Module Conflicts**: none known.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/chatdamagebuttons-betterrolls](https://github.com/syl3r86/chatdamagebuttons-betterrolls)

### Description
A small module to add "Apply Damage" buttons to Red Reigns Better Rolls 5e Module, based on hookings Chat Damage Buttons.
To install use the following link in Foundrys Module Setup
* https://raw.githubusercontent.com/syl3r86/chatdamagebuttons-betterrolls/master/chatdamagebuttons-betterrolls5e/module.json

---

## DDB Popper

* **Author**: errational#2007 on discord
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.4
* **System Compatibility (If applicable)**: dnd5e
* **Module Requirement(s)**: N/A
* **Module Conflicts**: N/A
* **Translation Support**: EN (full)

### Link(s) to Module
* https://github.com/eclarke12/fvtt-modules/tree/master/ddb-popper
* [Download](https://github.com/eclarke12/fvtt-modules/raw/master/ddb-popper.zip)

### Description
Opens a D&D Beyond popup for a linked actor. More info here: https://github.com/eclarke12/fvtt-modules/tree/master/ddb-popper

---

## DnD Beyond Character Importer

* **Author**: @Sillvva#2532 on Discord.
* **Version**: 0.19
* **Foundry VTT Compatibility**: 0.3+ (See Description)
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None.
* **Module Conflicts**: None, but see description.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/sillvva/foundry-vtt-modules/](https://github.com/sillvva/foundry-vtt-modules/) 

The module is available under the 'ddb-importer' directory.

### Description
This module allows you to import character data from DnD Beyond into Foundry Virtual Tabletop.  

The module has not been updated recently by its creator, but the community has produced a fix for this issue.  The fix is not included in the zip file for the module, but is instead contained within the Github repository, and must be retrieved there. Replace the file in the module folder with the fixed version.

---

## Favourite Item Tab

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de
* **Version**: 0.4
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None
* **Module Conflicts**: None known
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/favtab](https://github.com/syl3r86/favtab)

### Description
Adds a Favourite tab to display a customized list of items, feats and spells. Usable with the default dnd5e Character sheet. You can add any item from the inventory, spell book or feature section of the character sheet. This module also gives access to item charges. You can add these to any item on the favourite list or remove them by changing the maximum to 0. This uses the same data that is used by Moerill#7205's adnd5e module, since this data is not supported by default.

---

## Group Roll

* **Author**: trdischat#2123 on Discord.
* **Version**: 0.0
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition.
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/trdischat/fvtt/tree/master/grouproll](https://github.com/trdischat/fvtt/tree/master/grouproll) 

### Description
Implements group ability and skill check rolls per Player's Handbook, page 175: "*If at least half the group succeeds, the whole group succeeds.*" Modules also includes patches to implement the Halfling Lucky trait, and a house rule to use the average of 2d20 for normal skill and ability check rolls. Both of these patches can be disabled in config.js. All patches rely on the included `patchClass` utility function.

---

## Item Sheet Buttons

* **Author**: hooking#0492 on Discord.
* **Version**: 0.13
* **Foundry VTT Compatibility**: 0.2.8-0.2.10
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None.
* **Module Conflicts**: None currently known, but according to Github page may be prone to breaking in the future.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/hooking/foundry-vtt---item-sheet-buttons](https://gitlab.com/hooking/foundry-vtt---item-sheet-buttons) 

### Description
This module adds item card buttons into the description of items, so that the item cards do not need to be pinged in chat. It does have the side effect of making it harder to ping item descriptions within chat.

To install, download the zip file included in the Github module directory. Extract the zip folder to `/public/modules`. Restart Foundry Virtual Tabletop.

---
## Minor QOL Improvements

* **Author**: @tposney#1462 on Discord
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.3.6+
* **System Compatibility (If applicable)**: All
* **Module Requirement(s)**: None
* **Module Conflicts**: Does not work with the default Apply damage pull down but provides chat damage buttons instead.
* **Translation Support**: English, but localization support is included.

### Link(s) to Module
* https://gitlab.com/tposney/minor-qol

manifest https://dl.dropboxusercontent.com/s/yt34vrukyakkwqq/module.json

download https://dl.dropboxusercontent.com/s/ocd7la6gjasdl6t/minor-qol.zip


### Description
Add item deletion confirmation, accelerated dice rolls with attack and damage in one click and item info hiding. All features can be enabled/disabled from the in-game module settings. If enabling/disabling speed-item-rolls should should reload the browser window.

To install past the mainfest link into the foundry "add a module" or download the zip and unzip in your module directory.

Many thanks to @Red Rein @Hooking for allowing me to pillage their code.

---

## Loot Sheet NPC (5e)

* **Author**: hooking#0492 on Discord.
* **Version**: v0.2.2
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/hooking/foundry-vtt---loot-sheet-npc](https://gitlab.com/hooking/foundry-vtt---loot-sheet-npc) 

### Description
This module adds an additional NPC sheet which can be used for loot containers such as chests. It also allows spells to be automatically converted into spell scrolls by dragging them onto this sheet.

---

## NPC Browser

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de
* **Version: 0.1**
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None
* **Module Conflicts**: None known
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/npc-browser](https://github.com/syl3r86/npc-browser)

### Description
This module adds a search interface for actors. This enables more comfortable browsing and searching via predefined filters like challenge rating, type or ability score.

---

## Polymorpher

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.3.0+
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th edition.
* **Module Requirement(s)**: None.
* **Module Conflicts**: Previous version of the module deleted actors, do not use v0.1.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/polymorpher](https://github.com/syl3r86/polymorpher) 

### Description
A module for Foundry VTT that lets you polymorph characters into any other character! Just drag any Actor (NPC or Character) on top of another Actor to change the later into the prior. Support dropping both from Compendium or the sidebar.

---

## R20 Converter

* **Author**: KaKaRoTo#4756 on Discord. His Patreon can be found here: [https://www.patreon.com/kakaroto](https://www.patreon.com/kakaroto)
* **Version**: 0.3
* **Foundry VTT Compatibility**: 0.3.3
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None in Foundry, though module requires a campaign exported from Roll20 using KakaRoTo’s export tool.
* **Module Conflicts**: None known.
* **Translation Support**: EN (full)

### Link(s) to Module
* The module is paywalled, and requires subscribing to KaKaRoTo’s Patreon.

### Description 
This module imports most facets of a campaign, including scenes, dynamic lighting, basic sheet information, and more. It currently does not include thorough actor information (either for PCs or NPCs), or items. Bear in mind that exporting a campaign from Roll20 may violate the EULA.

---

## Roll20 NPC Importer, for 5e

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de
* **Version**: Roll20 NPC Importer 5e v0.5.1
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None.
* **Module Conflicts**: None known.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/roll20npcimporter](https://github.com/syl3r86/roll20npcimporter) 

### Description
This module allows for the importing of NPCs from Roll20, through use of JSONs exported via [VTT Enhancement Suite](https://ssstormy.github.io/roll20-enhancement-suite/). This import currently only supports NPCs created in the Roll20 OGL or Shaped version sheets. This module supports the Better NPC Sheet 5e, as well as the aDnD5e sheet in tagging actor items according to abilities, reactions, legendary actions, etc.  To install, first download the module, unzip it into `/public/modules`, and then restart Foundry while it is running.

---

## Sky's 5th Edition Dungeons & Dragons Sheet

* **Author**: Sky#9435
* **Version**: 0.0.2
* **Foundry VTT Compatibility**: 0.3.6+
* **System Compatibility**: D&D 5e
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: None

### Link(s) to Module
* [https://github.com/Sky-Captain-13/foundry/tree/master/sky5e](https://github.com/Sky-Captain-13/foundry/tree/master/sky5e)

### Description
This module provides a variant layout of the Core 5e Character Sheet in Foundry as well as providing some upgrades to various sections of the sheet.

* Rearranges the layout into a wider sheet, to display more information instead of being hidden behind tabs
* Enables rolling ability checks and saving throws directly instead of clicking through a popup
  * Best combined with Red Reign's BetterRoll5e module: https://github.com/RedReign/FoundryVTT-BetterRolls5e
* Adds the ability to click Known Languages under Traits to send the list to the chat window
* Adds Tool, Armor, and Weapon proficiencies beneath Skills
* Saves the scrollbar position when adding/deleting items from your inventory, features, or spellbook

---

## Spell Browser

* **Author**: Felix#6196 on Discord, syl3r31 on Github. He accepts donations on Paypal at felix.mueller.86@web.de.
* **Version**: 0.3
* **Foundry VTT Compatibility**: 0.3.0
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None
* **Module Conflicts**: None known.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/syl3r86/Spell-Browser](https://github.com/syl3r86/Spell-Browser)

### Description
This module adds a search interface for spells. This enables more comfortable browsing and searching via predefined filters like spell level, class or damage type.

---

## SRD Bestiary Module

* **Author**: DestinyGrey#2890, also known as “The_Entire_Eurozone”.  
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.2.8+
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition
* **Module Requirement(s)**: None, though it is compatible and has optional sorting tags for the Better NPC Sheet 5E module, as well as the aDnD5e module.  
* **Module Conflicts**: None (currently).  
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://drive.google.com/file/d/1oHMQhKuV-Vpdg5ftWTMaGZg76MVngZqO/view?usp=sharing](https://drive.google.com/file/d/1oHMQhKuV-Vpdg5ftWTMaGZg76MVngZqO/view?usp=sharing) 

### Description
This module includes each SRD NPC in 5th edition, imported into Foundry VTT. This includes all of their features, immunities/resistances/vulnerabilities, actions, and much, much more.  Other than lacking token images (token images do not appear to be part of the SRD), each NPC is built and ready for use in Foundry Virtual Tabletop.  Included in the module is a folder containing each individual NPC json, in case you wish to experiment with importing them, or future updates break the NPCs in this module. These can be imported individually using the Roll20 NPC Importer, for 5e module.  

Future updates will include edits to the imports to bring them in line with “good practice” for Foundry NPCs.

To install, simply extract the zip file into `/public/modules`, enable the module in Foundry, and then do a full restart in order to display the compendium.

---

## VTTA Party

* **Author**: solfolango77#0880 on Discord. His Patreon can be found here: [https://www.patreon.com/vttassets](https://www.patreon.com/vttassets) 
* **Version**: v1.0.0
* **Foundry VTT Compatibility**: 0.3.5+
* **System Compatibility (If applicable)**:
* **Module Requirement(s)**: None
* **Module Conflicts**:
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://www.vttassets.com/asset/vtta-party](https://www.vttassets.com/asset/vtta-party)

### Description
Successor to fvtt-party, which is discontinued as of now. Provides both an overview about the party in regards to AC, HP, and passive perception/investigation/insight and adds tooltips for the actors of the currently active scene.
Configurable options for granting players access to both features, or to use it for GMs only.

---

# Foundry VTT Modules for WFRP 4E

Foundry modules that work within Warhammer Fantasy Roleplay 4th Edition are noted here. These may include NPC compendiums that may be legally shared, world saves, character sheet mods, changes to roll tables, etc.

## Arcane Marks & Careers

* **Author**: Moo Man#7518 on Discord
* **Version**: 1.2.2
* **Foundry VTT Compatibility**: 0.3+
* **System Compatibility**: Warhammer Fantasy Roleplay 4th Edition.
* **Module Requirement(s)**: None
* **Module Conflicts**: None
* **Translation Support**: EN (full)

### Link(s) to Module
* https://github.com/moo-man/Arcane-Marks-Careers-FVTT

### Description
[This homebrew](https://drive.google.com/file/d/1uTy2r0EDMdcISFqqyxeIOSadtzz-OTAg/view) supplement I made adds Lore specific careers and marks for WFRP4e. 

This module for FVTT adds these careers and tables to the [WFRP4e system](https://github.com/CatoThe1stElder/WFRP-4th-Edition-FoundryVTT/tree/stable)

To install, simply add `arcane-marks-careers` into the modules folder in the `public` directory of Foundry. Enable the module in your world, then restart Foundry.

Once installed, you'll find the careers in the Arcane Careers Compendium, and you can roll on any Arcane Mark table with the chat command `/table <wind-name>`, e.g. `/table aqshy`.

---

# Foundry VTT Modules (Defunct)

Foundry VTT modules that no longer work are noted here. Modules included here have been defunct for at least one month. This exists to help document previous work on Foundry Virtual Tabletop by the community, as well as to exist as a record for anyone who chooses to remain on a previous version of Foundry VTT.  

## aDnD5e

* **Author**: Moerill#7205 on Discord
* **Version**: 0.2
* **Foundry VTT Compatibility**: 0.2.9-0.2.10
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition.
* **Module Requirement(s)**: None
* **Module Conflicts**: This module currently disables Better NPC Sheet 5e’s function in allowing NPC abilities and actions to be previewed within the sheet.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/moerills-fvtt-modules/adnd5e](https://gitlab.com/moerills-fvtt-modules/adnd5e) 

### Description
This module expands upon the existing 5e system in Foundry VTT, adding alternative PC and NPC sheets, as well as changing the system of attacks and macros, and adds a compendium for all SRD monsters, set up for use with this module. The mod is effectively a massive expansion in the ability to edit sheets for the user’s purposes, and a revamp of how the 5E system works. It is backwards-compatible with the default sheet, and can be switched between the two as needed.

---

## Encumbrance Variant

* **Author**: hooking#0492 on Discord.
* **Version**: 0.14
* **Foundry VTT Compatibility**: 0.2.8-0.2.10
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition.
* **Module Requirement(s)**: None.
* **Module Conflicts**: None currently known.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/hooking/foundry-vtt---encumbrance-variant-5e](https://gitlab.com/hooking/foundry-vtt---encumbrance-variant-5e) 

### Description
This module modifies how the encumbrance bar in the actor sheet is displayed to distinguish the different levels of encumbrance when using the variant rules in **PHB pg. 175**. It does not currently support the Powerful Build feature, as doing so would require extending the base Actor5eSheet class.

---

## FVTT-Party (Discontinued, see VTTA-Party for an successor)

* **Author**: @solfolango77#0880 on Discord.
* **Version**: 0.1
* **Foundry VTT Version Compatibility**: 0.3+
* **System Compatibility (If applicable)**: Dungeons and Dragons 5th Edition.
* **Module Requirement(s)**: None
* **Module Conflicts**: None known, although module is a WIP.
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/shwill/fvtt-party](https://github.com/shwill/fvtt-party) 

### Description
This module adds a convenient button to the actor’s tab, which will track the HP, AC, and Passive Perception, Investigation, and Insight of tokens on the Canvas. Currently a WIP, and may exhibit some bugs.

To install the module, download the zip file included in the Github module directory. Extract the zip file to `/public/modules`. Restart Foundry Virtual Tabletop.

---

# Appendix

## Appendix A: Adding a Module

**Copy and paste the outline below in writing up new module descriptions, formatting and all!**
```
## (Module Name)

* **Author**: (Put author’s name here, including Discord username. If they accept contributions in code or donations, note this here as well.)
* **Version**: (Note current version of module here.)
* **Foundry VTT Compatibility**: (Note which versions of Foundry Virtual Tabletop the module is compatible with.)
* **System Compatibility (If applicable)**: (Note which systems of Foundry Virtual Tabletop the module is compatible with.)
* **Module Requirement(s)**: (If the module requires other modules to function, note them here.)
* **Module Conflicts**: (If the module conflicts with other modules, either partially or completely, note conflicts here.)
* **Translation Support**: (Note which languages are supported, and if they have (full) or (partial) translations.

### Link(s) to Module
* (Put a web URL here to find the module.)

### Description
(Describe the module here. This should include the module’s function, installation instructions, and anything important to note. Due to the particular oddities of some archiving programs (WinRar, 7zip), and GitHub zip folders, including a screenshot of what the module should look like file-wise in the “public/modules/examplemodule” is appreciated, though not required.)

---
```

## Appendix B: Best Editing Practices

- Ideally, the term module should be used over mod, unless it is in the mod’s name or the author’s description. Mod can carry connotations from other games that might not exist in Foundry VTT, while modules in Foundry VTT can range from NPC compendiums, to worlds, to “enhancement suite” functions. They’re effectively the same thing, but it helps to emphasize how flexible Foundry Virtual Tabletop is. 
- Links to modules should link to the author’s page for it, if such exists. This helps emphasize the module author’s control over their creation, and allows users to see information that the module author deems important. If you have the module author’s permission otherwise, or you are the creator, feel free to link directly to the module download link. 
- Modules are sorted by system compatibility, then function, and then alphabetically. If a module is compatible with more than one system, but not “universally” in Foundry Virtual Tabletop, note compatibility in each system’s section. Otherwise, if a module is compatible universally, list it in the appropriate section for “universal modules”. 
- Ensure that Foundry is noted as “Foundry VTT” or “Foundry Virtual Tabletop” in writing, unless it is the module title, or the module author desires otherwise in the description. This helps emphasize Foundry’s role as a unique, standalone tabletop, and helps distinguish it from other brands using the word “foundry”.   
- Ideally, each module should be separated by a single line break. This is just to help it look neat. 
- Modules should not be listed if they violate existing copyright law.  
