Let's start by taking a look a the BoilerplateActor class in `/module/actor/actor.js`. As with previous examples, you'll want to rename `BoilerplateActor` to whatever your system's name is, such as `MySystemNameActor`.

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

We're doing a few things in here. First, we're using `export` on this class so that it's available to our main ES module file for importing. Secondly, we're extending the base `Actor` class that Foundry provides so that we get all of the logic that comes along with that by default.

We can override any method in the [Actor class](https://foundryvtt.com/api/Actor.html), but in this case we're just overriding the `prepareData()` method.

## Basic data vs. derived data

So, what's the difference between basic data and derived data? Basic data are things that you define in your `template.json` file and should be editable on the character sheet. For example, ability scores in D&D would be basic data.

Derived data is the kind of data that you don't actually store and instead calculate it when you need it. For example, ability modifiers are based on applying a formula to ability scores, so we have no reason to make the user enter those manually. Because of that, we need to create those values in the `prepareData()` method.

## Creating derived values with prepareData()

`prepareData()` can be used to prepare additional data at runtime that we don't necessarily have defined in our main `template.json` file.

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

First, we're using `super.prepareData()` to continue using the main Actor class' original prepareData() method.

Second, we're making a few convenience variables related to the actor. Those are `actorData`, `data`, and `flags`. These are optional, but without them you'll be doing stuff like `this.data.data.abilities.value`, which can get confusing.

> **What's up with `data.data`?**
> Some data is always included regardless of system, like `name` and is accessible at `actor.data.name`, while your system's unique properties are stored in a nested data property, such as `actor.data.data.abilities.str`.

Third, we're checking to see what type of actor this is. If this is a character, we run it through a custom method that we've created called `_prepareCharacterData()` to prepare additional derived values. We could also do the same for things like NPCs if we had a need to.

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

You could put any sort of logic in this method! In this case, we know that the Boilerplate system has an `abilities` property in its data model, so we're looping through it. The syntax is a bit tricky for the actual loop, but `Object.entries` will return pairs of key/value items for whatever apply it to, and when we loop through that each loop will have a `key` that would be the label such as `str` or `dex` and also an `ability` which would be the ability object.

In this case the ability object only has a `value` property, so we then use some math based on the d20 rules to calculate what the ability modifier should be and assign it to `ability.mod`.

And with that, we're done deriving new values! We don't have to return anything; because we're working with objects and we didn't clone or copy them, the changes we made to `ability.mod` will automatically work their way back up to the original `actorData` object.

---

- **Prev:** [Creating your main system javascript file](https://foundry-vtt-community.github.io/wiki/SD05-Creating-your-main-JS-file)
- **Next:** [Extending the ActorSheet class](https://foundry-vtt-community.github.io/wiki/SD07-Extending-ActorSheet-class)