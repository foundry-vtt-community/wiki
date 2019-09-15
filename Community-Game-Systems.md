<!--tl=2-->
<!--ts-->
   * [Dungeons &amp; Dragons](#dungeons--dragons)
      * [D&amp;D5e](#dd5e)
   * [Pathfinder](#pathfinder)
      * [Pathfinder 2e](#pathfinder-2e)
   * [Warhammer Fantasy](#warhammer-fantasy)
      * [WFRP 4E System](#wfrp-4e-system)
   * [Appendix](#appendix)
      * [Appendix A: Adding a Game System](#appendix-a-adding-a-game-system)
      * [Appendix B: Best Editing Practices](#appendix-b-best-editing-practices)
<!--te-->

# Dungeons & Dragons

## D&D5e

* **Author**: Atropos (Foundry VTT Core Developer)
* **Version**: 0.61
* **Foundry VTT Compatibility**: 0.3.0+
* **Translation Support**: EN (full)

### Link(s) to Game System
* https://gitlab.com/foundrynet/dnd5e

### Description
An implementation of the Dungeons & Dragons 5th Edition ruleset under the OGL. This system currently comes bundled with Foundry VTT, but in the future may be distributed separately. Please feel free to post issues or pull requests to the GitLab repo for my consideration.

---

# Pathfinder

Foundry systems for the various Pathfinder editions.

## Pathfinder 2e

* **Author**: hooking#0492 on Discord
* **Version**: Alpha 0.21
* **Foundry VTT Compatibility**: 0.3+
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://gitlab.com/hooking/foundry-vtt---pathfinder-2e/](https://gitlab.com/hooking/foundry-vtt---pathfinder-2e/)

### Description
This system adds support for Pathfinder Second Edition to Foundry VTT.

Please Note:
- Functionality is not complete with plenty of work remaining.
- This is a fork of the dnd5e system so there may still be references to dnd5e in places and the assets from 5e are included for now (I plan to use them soon).
- If you find any issues or have any feedback please let me know.

Known Issues:
- AC is not automatically calculated, Just enter it in the input field.
- Critical damage is not calculated currently.

To install the system, follow these instructions:
1. Download the zip file included in the system directory.
1. Extract the included folder to public/systems in your Foundry Virtual Tabletop installation folder.
1. Restart Foundry Virtual Tabletop.

---

# Warhammer Fantasy

Foundry systems for the various Warhammer Fantasy Roleplay editions.

## WFRP 4E System

* **Author**: @Moo Man#7518 and @CatoThe1stElder#9725 on Discord
* **Version**: Beta 0.8.2
* **Foundry VTT Compatibility**: 0.3+ (Highly recommend players use Chrome, Firefox doesn't display the sheet correctly).
* **Translation Support**: EN (full)

### Link(s) to Module
* [https://github.com/CatoThe1stElder/WFRP-4th-Edition-FoundryVTT](https://github.com/CatoThe1stElder/WFRP-4th-Edition-FoundryVTT/tree/stable) 

### Description
Installing this system allows you to create campaigns in the grim and perilous world of Warhammer Fantasy 4th edition!

To install, use the in-app installer and enter into the manifest URL: `https://raw.githubusercontent.com/CatoThe1stElder/WFRP-4th-Edition-FoundryVTT/stable/system.json`

---

# Appendix

## Appendix A: Adding a Game System

**Copy and paste the outline below in writing up new game system descriptions, formatting and all!**
```
## (Game System Name)

* **Author**: (Put author’s name here, including Discord username. If they accept contributions in code or donations, note this here as well.)
* **Version**: (Note current version of game system here.)
* **Foundry VTT Compatibility**: (Note which versions of Foundry Virtual Tabletop the game system is compatible with.)
* **Translation Support**: (Note which languages are supported, and if they have (full) or (partial) translations.

### Link(s) to Game System
* (Put a web URL here to find the game system.)

### Description
(Describe the game system here. This should include the game system’s function, installation instructions, and anything important to note. Due to the particular oddities of some archiving programs (WinRar, 7zip), and GitHub zip folders, including a screenshot of what the module should look like file-wise in the “public/systems/examplesystem” is appreciated, though not required.)

---
```

## Appendix B: Best Editing Practices

- Links to game systems should link to the author’s page for it, if such exists. This helps emphasize the game system author’s control over their creation, and allows users to see information that the game system author deems important. If you have the game system author’s permission otherwise, or you are the creator, feel free to link directly to the game system download link. 
- Game Systems are sorted by system compatibility, then function, and then alphabetically.
- Ensure that Foundry is noted as “Foundry VTT” or “Foundry Virtual Tabletop” in writing, unless it is the system title, or the module author desires otherwise in the description. This helps emphasize Foundry’s role as a unique, standalone tabletop, and helps distinguish it from other brands using the word “foundry”.   
- Ideally, each game system should be separated by a single line break. This is just to help it look neat. 
- Game Systems should not be listed if they violate existing copyright law.

