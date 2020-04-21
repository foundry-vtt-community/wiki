# Available commands in chat : 
* Making a roll : `/r` or `/roll`. You can add a dash with custom text to use it as roll's flavor: `/roll 1d20+4+2 # Viciously attack that goblin`
* Making a roll to the GM only : `/gmr` or `/gmroll`
* Making a blind roll to the GM : `/br` or `/blindroll`
* In Character chat (triggers a chat bubble) : `/ic`
* Out of Character chat : `/occ`
* Emote : `/em` or `/emote`
* Whispers : `@PlayerName`, `@CharacterName`, `@[Player Name]`, or `@[Character Name]`

# Available markup in chat :
* Inline dice rolling: `For this, I roll [[1d20]] mid-chat!`, `[[2d20kh]]` (kh = "keep high"), etc.
* Entry/Object links:
  * Scene : `Check out @Scene[Old Road Ambush].`
  * Actor : `Is it a @Actor[Kobold]?`
    Note there must be an _actor_ that exists with that name.  Not just a Compendium entry.
  * Item : `You find an @Item[Abacus].`
    As with actor references, this refers to an item (see item sidebar).  A Compendium entry isn't enough.
  * Journal Entry : `Take a look at @JournalEntry[Exhaustion] for more details.`
  * Roll Table : `/whisper AssistantGm Use @RollTable[Wilderness Encounters] for tonight.`
  * Macro : `Try @Macro[State Targets]`
    Assumes there's a macro named "State Targets".

Note entry/object links are case-sensitive!  Both the type ("JournalEntry", not "journalEntry") and the object's name ("Abacus", not "abacus").  You can also drag-and-drop objects to some places to create links.

In the case of Actor, Item, and other references of the `@<type>[<name>]` style, a reference is created to a specific object's ID.  If that object is later deleted, even if a new one with the same name is made, the existing link won't refer to the new object.  Also note that if multiple choices for a given name exist, the "first" one will be picked.  If that "first" one happens to be one that a player can't see due to permissions, then even if there's a "second" one the player can see, clicking the reference link will give them a permissions error.

# Rolling dice

General information can be found in [Knowledge Base](https://foundryvtt.com/article/dice/), but not all features are described there:
* Some functions of JS builtin object [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) are supported in rolls. Example `[[ 1d6 + round(7/2) ]]`
* Inline rolls can be deferred by adding slash-command after opening brackets. Example: `Make either dexterity based roll [[/roll 1d20 + @abilities.dex.mod ]] or str based roll [[/roll 1d20 + @abilities.str.mod ]]`
* Explode with "operator" does not really need a number after operator and maximum die value is used in that case. Example: `/roll 1d4x=` will explode on 4.