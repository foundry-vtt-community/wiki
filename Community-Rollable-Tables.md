<!--tl=2-->
<!--ts-->
   * [Foundry VTT Rollable Tables for DnD 5E](#foundry-vtt-rollable-tables-for-dnd-5e)
      * [Potion Strength](#potion-strength)
   * [Appendix](#appendix)
      * [Appendix A: Adding a Rollable Table](#appendix-a-adding-a-rollable-table)
      * [Appendix B: Best Editing Practices](#appendix-b-best-editing-practices)
      * [Appendix C: Importing &amp; Exporting Tables](#appendix-c-importing--exporting-tables)
<!--te-->

# Foundry VTT Rollable Tables for DnD 5E

Foundry rollable tables that work within Dungeons and Dragons 5th Edition are noted here.

## Potion Strength

* **Author**: Sneaky#0526 on Discord
* **Version**: 0.1
* **Table Type**: Text
* **Table Entries**: 1d10
* **Translation Support**: EN (Full)

### Description
Based on u/olirant's [tables for generating potions randomly](https://www.reddit.com/r/DnDBehindTheScreen/comments/4btnkc/random_potions_table/).

### Table Data

```
{"_id":"aS9SxiRDo63s9ZYp","name":"Potion Strength","permission":{"default":0},"folder":null,"sort":300001,"flags":{},"results":[{"id":1,"flags":{},"type":0,"text":"Regular with slight side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[1,1],"drawn":false},{"id":2,"flags":{},"type":0,"text":"Regular with no side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[2,2],"drawn":false},{"id":3,"flags":{},"type":0,"text":"Regular with strong side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[3,3],"drawn":false},{"id":4,"flags":{},"type":0,"text":"Minor with strong side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[4,4],"drawn":false},{"id":5,"flags":{},"type":0,"text":"Minor with a slight side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[5,5],"drawn":false},{"id":6,"flags":{},"type":0,"text":"Major with a strong side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[6,6],"drawn":false},{"id":7,"flags":{},"type":0,"text":"Major with a small side effect","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[7,7],"drawn":false},{"id":8,"flags":{},"type":0,"text":"A poison with almost no positive effects","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[8,8],"drawn":false},{"id":9,"flags":{},"type":0,"text":"Temporary but strong and wears off quickly","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[9,9],"drawn":false},{"id":10,"flags":{},"type":0,"text":"Seemingly Permanent","img":"icons/svg/d20-black.svg","resultId":"","weight":1,"range":[10,10],"drawn":false}],"formula":"","replacement":true,"displayRoll":true}
```

---

# Appendix

## Appendix A: Adding a Rollable Table

**Copy and paste the outline below in writing up new tables, formatting and all!**
```
## (Table Name)

* **Author**: (Put author’s name here, including Discord username. If they accept contributions in code or donations, note this here as well.)
* **Version**: (Note current version of the table here.)
* **Table Type**: (Put the type of table here)
* **Table Entries**: (Put the number of table entries here)
* **Translation Support**: (Note which languages are supported, and if they have (full) or (partial) translations.

### Description
(Describe the table here. This should include anything important to note.)

### Table Data

(Enter table data here and surround with code blocks, three ` at the start and end of the table data. You can find your table data at \resources\app\public\worlds\(your world)\data, in the tables.db file)


---
```

## Appendix B: Best Editing Practices

- Links to rollable tables should link to the author’s page for it, if such exists. This helps emphasize the table author’s control over their creation, and allows users to see information that the table author deems important. If you have the table author’s permission otherwise, or you are the creator, feel free to link directly to the adventure download link. 
- Tables are sorted by system compatibility and then alphabetically.
- Ensure that Foundry is noted as “Foundry VTT” or “Foundry Virtual Tabletop” in writing. This helps emphasize Foundry’s role as a unique, standalone tabletop, and helps distinguish it from other brands using the word “foundry”.   
- Ideally, each table should be separated by a single line break. This is just to help it look neat. 
- Tables should not be listed if they violate existing copyright law.

## Appendix C: Importing & Exporting Tables

- Table Data is stored at `\resources\app\public\worlds\(your world)\data` in the `tables.db` file
- All of the data for a table is stored on a single line
**Exporting**
- To export table data just: select, copy, and paste the line with the table you want to export
**Importing**
- To import table data just: copy the data of the table you want, paste the data as a new line in the `tables.db` file
