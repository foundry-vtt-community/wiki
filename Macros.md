# What is a Macro?
A macro is a set of commands (such as a roll, a message, or a Javascript scriptlet) that Foundry can execute when the associated macro button is pressed.

Macros were added in Foundry VTT version `0.4.4`

# Macro Types
## Chat Macros

### Examples

## Script Macros

### Examples
#### Random Table Roll 

```js
const table = game.tables.entities.find(t => t.name === "MY TABLE NAME");
table.draw();
```

Replace the table name with the one you want to use.

