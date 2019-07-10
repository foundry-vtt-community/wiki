# Setting up Worlds

This is the World configuration screen, used to create and update worlds.

When creating a new world, you must fill in some mandatory details. The world name is a human-readable string that may contain special characters. The file path to your world defines the subdirectory name within the `public/worlds` folder where your world will be saved.

**⚠️ Warning**
> The file path for your world will be used in web URLs, so it is best to adhere to common web standards in choosing this name. Avoid spaces or special characters, instead using hyphens to separate multiple terms.

You must choose the Game System that your world will use. Foundry VTT comes with some common game systems built-in, but more game systems are available through our excellent community of mod developers. To install a new game system, simply download the system definition and extract it within the `public/systems folder`. For a new system to be recognized by the software you must restart the application.

**⚠️ Warning**
> A world’s game system cannot be changed once the world is created, since any data created in that world will use the data model and schema for that system.

Lastly, you may provide a text description of your World that can be used to keep track of details about the world or advertise it to potential players.