<!--tl=4-->
<!--ts-->
   * [What is a Macro?](#what-is-a-macro)
      * [Community Contributed Macros](#community-contributed-macros)
   * [Macro Types](#macro-types)
      * [Chat Macros](#chat-macros)
      * [Script Macros](#script-macros)
         * [Script Macros Examples](#script-macros-examples)
            * [Random Table Roll](#random-table-roll)
            * [Rolling a skill check for DnD 5e](#rolling-a-skill-check-for-dnd-5e)
            * [Rolling an attribute check for DnD 5e](#rolling-an-attribute-check-for-dnd-5e)
            * [Play Audio](#play-audio)
<!--te-->

# What is a Macro?
A macro is a set of commands (such as a roll, a message, or a Javascript scriptlet) that Foundry can execute when the associated macro button is pressed.

Macros were added in Foundry VTT version `0.4.4`

## Community Contributed Macros
A community-contributed repository of Macros can be found here: [github](https://github.com/foundry-vtt-community/macros).

# Macro Types
## Chat Macros

Chat macros are chat commands that have been saved for later reuse. See section on [Chat commands](https://foundry-vtt-community.github.io/wiki/Chat/)

## Script Macros

Script Macros in Foundry use the underlying [JavaScript API](https://foundryvtt.com/api) to execute various commands. The API respects the permissions of the user executing the macro, so players cannot delete your big bad evil guy for example.

See also: [Learning API](https://foundry-vtt-community.github.io/wiki/API-Learning-API/), and [API Snippets](https://foundry-vtt-community.github.io/wiki/API-Snippets/) (many of them can be used in a Macros)
Some examples of using script macros follows.

### Script Macros Examples

#### Random Table Roll 

```js
const table = game.tables.entities.find(t => t.name === "MY TABLE NAME");
table.draw();
```

Replace the table name with the one you want to use.

#### Rolling a skill check for DnD 5e

Here are a few simple scripts useful for rolling skill checks using the dnd5e system.

```js
// This would roll an athletics skill check for the players character. 
// Just replace 'ath' with the appropriate skill abbreviation for the
// skill you'd like to roll.
character.rollSkill('ath');

// This would be used if a player controls more than one character.
// It would roll the check for which ever token the player has selected.
actor.rollSkill('ath');
```

List of skill abbreviations:

* "acr" => Acrobatics
* "ani" => Animal Handling
* "arc" => Arcana
* "ath" => Athletics
* "dec" => Deception
* "his" => History
* "ins" => Insight
* "itm" => Intimidation
* "inv" => Investigation
* "med" => Medicine
* "nat" => Nature
* "prc" => Perception
* "prf" => Performance
* "per" => Persuasion
* "rel" => Religion
* "slt" => Sleight of Hand
* "ste" => Stealth
* "sur" => Survival

#### Rolling an attribute check for DnD 5e

These are examples for rolling an attribute check.

```js
// This would pop up a dialog asking if you'd like
// to roll a Strength Test or a Strength Save.
// Just replace "str" with the appropriate ability
// abbreviation.
character.rollAbility("str");

// or this for a player that is controlling multiple
// tokens.
actor.rollAbility("str");

// This would skip the dialog and roll an ability test
character.rollAbilityTest("str");

// And this would skip the dialog and roll an ability save
character.rollAbilitySave("str");
```

List of ability abbreviations:

* "str" => Strength
* "dex" => Dexterity
* "con" => Constitution
* "int" => Intelligence
* "wis" => Wisdom
* "cha" => Charisma

#### Play Audio
This is a direct way to play audio.

<!--- {% raw %} --->
```js
AudioHelper.play({src: "audio/SFX/Fire arrow.mp3", volume: 0.8, autoplay: true, loop: false}, true);
```
<!--- {% endraw %} --->

###Roll a die
This is a way to roll a die with a "script" macro instead of a chat macro.
<!--- {% raw %} --->
```js
const roll = new Roll(`1d6`);
roll.roll();
roll.toMessage({
    flavor: "Sneak Attack Damage",
});
```
<!--- {% endraw %} --->