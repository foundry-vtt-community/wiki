<!--tl=2-->
<!--ts-->
   * [Foundry VTT Tools (Universal)](#foundry-vtt-tools-universal)
      * [DunGen](#dungen)
      * [Foundry Project Creator (FPC)](#foundry-project-creator-fpc)
      * [Table Importer](#table-importer)
   * [Appendix](#appendix)
      * [Appendix A: Adding a Tool](#appendix-a-adding-a-tool)
      * [Appendix B: Best Editing Practices](#appendix-b-best-editing-practices)
<!--te-->

# Foundry VTT Tools (Universal)

Foundry tools that work across all or most systems are noted here. These differ from modules as they are not integrated or loaded into Foundry VTT, but instead work externally and provide you with files or code you can import, such as a scene file.

## DunGen

* **Author**: Nick#2947 on Discord. His Patreon can be found here: [patreon.com/DungeonChannel](https://www.patreon.com/DungeonChannel)
* **Version**: 0.9
* **Foundry VTT Compatibility**: 0.6.0
* **Translation Support**: EN (full)

### Link(s) to Tool
* [https://DunGen.app](https://dungen.app/dungen/)

### Description
DunGen is a Dungeon Generator that creates high resolution maps ready to import into Foundry VTT. Alongside the maps, you can also generate a full scene file including pre-built walls to take full advantage of Foundry's lighting feature in only a minute. You can see it in action in [this short video](https://youtu.be/2RlPpLOFkhc).

---

## FG Converter

* **Author**: grape_juice#2539 on Discord
* **Version**: 0.0.1
* **Foundry VTT Compatibility**: 0.6.0+

### Link(s) to Tool
* [Link to the repository](hhttps://gitlab.com/jesusafier/fg_converter)
* [Link to the Patreon](https://www.patreon.com/foundry_grape_juice)

### Description
Converts Fantasy Grounds campaigns into FoundryVTT worlds.

Current Generic Support Status: (This works for all game systems)

✅ Refence Manuals and Books display
✅ Scenes including walls and doors (even for FGC)
✅ Journals
✅ Journals on Scenes (map pins)
✅ Rollable tables
✅ Image asset de-noise and upscalling Token Example, Map Example (FG has "optimized" image assets that look really bad in modern VTTs)
✅ Token placement on scenes

---

## Foundry Project Creator (FPC)

* **Author**: Nick van Oosten (NickEast#1131 on Discord)
* **Version**: 1.3.0
* **Foundry VTT Compatibility**: 0.4.5+

### Link(s) to Tool
* [Link to the repository](https://gitlab.com/foundry-projects/foundry-pc/create-foundry-project)
* [Link to the wiki](https://gitlab.com/foundry-projects/foundry-pc/create-foundry-project/-/wikis/home)

### Description
The **Project Creator** is a tool to quickly get started with developing modules and systems for the Foundry VTT. It provides basic boilerplate code, for both vanilla JavaScript as well as TypeScript, and automated tasks using Gulp to speed up building, testing, and releasing your module.

Please refer to the README and the FPC wiki for more information.

---

## Table Importer

* **Author**:`_Joe_#5581` on Discord
* **Version**: 0.1
* **Foundry VTT Compatibility**: 0.6

### Link(s) to Tool
[Link to the repo](https://github.com/jennis0/foundryvtt-utils/)

### Description
A python3 script to process tables copied from online sources into a FoundryVTT compatible JSON format. It has several particularly useful features:
* Auto subtable generation
* Auto generation of multiple tables from NxM arrays
* Dice roll formatting
* Output a single table as an importable RollTable json file
* Output many tables as a (nearly) nicely importable compendium format
* better-rolltables integration with automatic table embedding and smart handling of currency

---

App

# Appendix

## Appendix A: Adding a Tool

**Copy and paste the outline below in writing up new tool descriptions, formatting and all!**
```
## (Tool Name)

* **Author**: (Put author’s name here, including Discord username. If they accept contributions in code or donations, note this here as well.)
* **Version**: (Note current version of module here.)
* **Foundry VTT Compatibility**: (Note which versions of Foundry Virtual Tabletop the module is compatible with.)
* **System Compatibility (If applicable)**: (Note which systems of Foundry Virtual Tabletop the tool is compatible with.)
* **Translation Support**: (Note which languages are supported, and if they have (full) or (partial) translations.

### Link(s) to Tool
* (Put a web URL here to find the tool.)

### Description
(Describe the tool here. This should include the tool’s function, installation instructions, and anything important to note.)

---
```

## Appendix B: Best Editing Practices

- The term tool should be used when denoting a third-party program or website that interacts with Foundry VTT.
- Ideally, the term module should be used over mod when necessary, unless it is in the mod’s name or the author’s description. Mod can carry connotations from other games that might not exist in Foundry VTT, while modules in Foundry VTT can range from NPC compendiums, to worlds, to “enhancement suite” functions. They’re effectively the same thing, but it helps to emphasize how flexible Foundry Virtual Tabletop is. 
- Links to tools should link to the author’s page for it, if such exists. This helps emphasize the tool author’s control over their creation, and allows users to see information that the tool author deems important. If you have the tool author’s permission otherwise, or you are the creator, feel free to link directly to the tool download link, if any.
- Tools are sorted by system compatibility, then function, and then alphabetically. If a tool is compatible with more than one system, but not “universally” in Foundry Virtual Tabletop, note compatibility in each system’s section. Otherwise, if a tool is compatible universally, list it in the appropriate section for “universal tools”. 
- Ensure that Foundry is noted as “Foundry VTT” or “Foundry Virtual Tabletop” in writing, unless it is the tool title, or the tool author desires otherwise in the description. This helps emphasize Foundry’s role as a unique, standalone tabletop, and helps distinguish it from other brands using the word “foundry”.   
- Ideally, each tool should be separated by a single line break. This is just to help it look neat. 
- Tools should not be listed if they violate existing copyright law.  
