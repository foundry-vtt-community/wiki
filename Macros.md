# What is a Macro?
A macro is a set of commands (such as a roll, a message, or a Javascript scriptlet) that Foundry can execute when the associated macro button is pressed.

Macros were added in Foundry VTT version `0.4.4`

Some community contributed Macros can be found on [github](https://github.com/foundry-vtt-community/macros).

# Macro Types
## Chat Macros

(needs content)

## Script Macros

Script macros are written in JavaScript and can utilize [API](https://foundryvtt.com/api/) objects and methods (like `game.users`, `canvas.tokens`, or `game.user.character`). When a token is selected before calling a macro, then `token` variable will also be available for code in macro. 

[Examples](Script-Macros)

See also: [API Snippets](API-Snippets) (many of them can be used in a Macros)

