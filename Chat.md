# Available commands in chat : 
* Making a roll : `/r` or `/roll`
* Making a roll to the GM only : `/gmr` or `/gmroll`
* Making a blind roll to the GM : `/br` or `/blindroll`
* In Character chat (triggers a chat bubble) : `/ic`
* Out of Character chat : `/occ`
* Emote : `/em` or `/emote`
* Whispers : `@PlayerName`, `@CharacterName`, `@[Player Name]`, or `@[Character Name]`

# Available markup in chat :
* Dice rolling : `For this, I roll [[1d20]] mid-chat!`, `[[2d20kh]]` (kh = "keep high"), etc.
* Actor references : `Is it a @Actor[Kobold]?`
  Note there must be an _actor_ that exists with that name.  Not just a Compendium entry.
* Item references : `You find an @Item[Abacus].`
  As with actor references, this refers to an item (see item sidebar).  A Compendium entry isn't enough.
* Macro references : `Try @Macro[State Targets]`
  Assumes there's a macro named "State Targets".
* Scene references : `Check out @Scene[Old Road Ambush].`

In the case of Actor, Item, and other references of the `@<type>[<name>]` style, a reference is created to a specific object's ID.  If that object is later deleted, even if a new one with the same name is made, the existing link won't refer to the new object.  Also note that if multiple choices for a given name exist, the "first" one will be picked.  If that "first" one happens to be one that a player can't see due to permissions, then even if there's a "second" one the player can see, clicking the reference link will give them a permissions error.