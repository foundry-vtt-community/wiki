Let's start by taking a look a the BoilerplateActor class in <!-- {% raw %} -->`/module/actor/actor.js`<!-- {% endraw %} -->. As with previous examples, you'll want to rename <!-- {% raw %} -->`BoilerplateActor`<!-- {% endraw %} --> to whatever your system's name is, such as <!-- {% raw %} -->`MySystemNameActor`<!-- {% endraw %} -->.

<!--- {% raw %} --->

```js
/**
 * Extend the base Actor entity by defining a custom roll data structure which is ideal for the Simple system.
 * @extends {Actor}
 */
export class BoilerplateActor extends Actor {

  /**
   * Augment the basic actor data with additional dynamic data.
   */
  prepareData() {
    super.prepareData();

    const actorData = this.data;
    const data = actorData.data;
    const flags = actorData.flags;

    // Make separate methods for each Actor type (character, npc, etc.) to keep
    // things organized.
    if (actorData.type === 'character') this._prepareCharacterData(actorData);
  }

  /**
   * Prepare Character type specific data
   */
  _prepareCharacterData(actorData) {
    const data = actorData.data;

    // Make modifications to data here. For example:

    // Loop through ability scores, and add their modifiers to our sheet output.
    for (let [key, ability] of Object.entries(data.abilities)) {
      // Calculate the modifier using d20 rules.
      ability.mod = Math.floor((ability.value - 10) / 2);
    }
  }

}
```

<!--- {% endraw %} --->

We're doing a few things in here. First, we're using <!-- {% raw %} -->`export`<!-- {% endraw %} --> on this class so that it's available to our main ES module file for importing. Secondly, we're extending the base <!-- {% raw %} -->`Actor`<!-- {% endraw %} --> class that Foundry provides so that we get all of the logic that comes along with that by default.

We can override any method in the [Actor class](https://foundryvtt.com/api/Actor.html), but in this case we're just overriding the <!-- {% raw %} -->`prepareData()`<!-- {% endraw %} --> method.

## Basic data vs. derived data

So, what's the difference between basic data and derived data? Basic data are things that you define in your <!-- {% raw %} -->`template.json`<!-- {% endraw %} --> file and should be editable on the character sheet. For example, ability scores in D&D would be basic data.

Derived data is the kind of data that you don't actually store and instead calculate it when you need it. For example, ability modifiers are based on applying a formula to ability scores, so we have no reason to make the user enter those manually. Because of that, we need to create those values in the <!-- {% raw %} -->`prepareData()`<!-- {% endraw %} --> method.

## Creating derived values with prepareData()

`prepareData()`<!-- {% endraw %} --> can be used to prepare additional data at runtime that we don't necessarily have defined in our main <!-- {% raw %} -->`template.json`<!-- {% endraw %} --> file.

Let's take a closer look at the prepareData() method:

<!--- {% raw %} --->

```js
/**
 * Augment the basic actor data with additional dynamic data.
 */
prepareData() {
  super.prepareData();

  const actorData = this.data;
  const data = actorData.data;
  const flags = actorData.flags;

  // Make separate methods for each Actor type (character, npc, etc.) to keep
  // things organized.
  if (actorData.type === 'character') this._prepareCharacterData(actorData);
}
```

<!--- {% endraw %} --->

First, we're using <!-- {% raw %} -->`super.prepareData()`<!-- {% endraw %} --> to continue using the main Actor class' original prepareData() method.

Second, we're making a few convenience variables related to the actor. Those are <!-- {% raw %} -->`actorData`<!-- {% endraw %} -->, <!-- {% raw %} -->`data`<!-- {% endraw %} -->, and <!-- {% raw %} -->`flags`<!-- {% endraw %} -->. These are optional, but without them you'll be doing stuff like <!-- {% raw %} -->`this.data.data.abilities.value`<!-- {% endraw %} -->, which can get confusing.

> **What's up with <!-- {% raw %} -->`data.data`?**
> Some data is always included regardless of system, like <!-- {% raw %} -->`name`<!-- {% endraw %} --> and is accessible at <!-- {% raw %} -->`actor.data.name`<!-- {% endraw %} -->, while your system's unique properties are stored in a nested data property, such as <!-- {% raw %} -->`actor.data.data.abilities.str`<!-- {% endraw %} -->.

Third, we're checking to see what type of actor this is. If this is a character, we run it through a custom method that we've created called <!-- {% raw %} -->`_prepareCharacterData()`<!-- {% endraw %} --> to prepare additional derived values. We could also do the same for things like NPCs if we had a need to.

### _prepareCharacterData()

Now that we've segmented off a custom method that can prepare character data without also affecting NPCs, let's calculate ability modifiers from ability scores.

<!--- {% raw %} --->

```js
/**
 * Prepare Character type specific data
 */
_prepareCharacterData(actorData) {
  const data = actorData.data;

  // Make modifications to data here. For example:

  // Loop through ability scores, and add their modifiers to our sheet output.
  for (let [key, ability] of Object.entries(data.abilities)) {
    // Calculate the modifier using d20 rules.
    ability.mod = Math.floor((ability.value - 10) / 2);
  }
}
```

<!--- {% endraw %} --->

You could put any sort of logic in this method! In this case, we know that the Boilerplate system has an <!-- {% raw %} -->`abilities`<!-- {% endraw %} --> property in its data model, so we're looping through it. The syntax is a bit tricky for the actual loop, but <!-- {% raw %} -->`Object.entries`<!-- {% endraw %} --> will return pairs of key/value items for whatever apply it to, and when we loop through that each loop will have a <!-- {% raw %} -->`key`<!-- {% endraw %} --> that would be the label such as <!-- {% raw %} -->`str`<!-- {% endraw %} --> or <!-- {% raw %} -->`dex`<!-- {% endraw %} --> and also an <!-- {% raw %} -->`ability`<!-- {% endraw %} --> which would be the ability object.

In this case the ability object only has a <!-- {% raw %} -->`value`<!-- {% endraw %} --> property, so we then use some math based on the d20 rules to calculate what the ability modifier should be and assign it to <!-- {% raw %} -->`ability.mod`<!-- {% endraw %} -->.

And with that, we're done deriving new values! We don't have to return anything; because we're working with objects and we didn't clone or copy them, the changes we made to <!-- {% raw %} -->`ability.mod`<!-- {% endraw %} --> will automatically work their way back up to the original <!-- {% raw %} -->`actorData`<!-- {% endraw %} --> object.

---

* **Prev:** [Creating your main system javascript file](https://foundry-vtt-community.github.io/wiki/SD05-Creating-your-main-JS-file)
* **Next:** [Extending the ActorSheet class](https://foundry-vtt-community.github.io/wiki/SD07-Extending-ActorSheet-class)