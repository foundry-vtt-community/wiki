When building a new system, you have several options to choose from. You can copy an existing system (depending on its license) like the Simple World-building system, you can use a system generator, or you could start from scratch and have total control.

## Option 1: Download

1. Download a zip version of the [Boilerplate System](https://gitlab.com/asacolips-projects/foundry-mods/boilerplate/-/archive/master/boilerplate-master.zip)
2. Extract it to the <!-- {% raw %} -->`/Data/systems`<!-- {% endraw %} --> directory in your Foundry userData folder and rename it from <!-- {% raw %} -->`boilerplate-master`<!-- {% endraw %} --> to your system's name (lowercase, machine-safe).
3. Search the directory for any files with the filename <!-- {% raw %} -->`boilerplate`<!-- {% endraw %} --> and rename them to your system's machine-safe name, such as <!-- {% raw %} -->`mysystemname`<!-- {% endraw %} -->.
4. Search the files for any occurrences of <!-- {% raw %} -->`Boilerplate`<!-- {% endraw %} --> (case-sensitive) and replace those with a capitalized version of your system name that's still machine-safe, such as <!-- {% raw %} -->`MySystemName`<!-- {% endraw %} -->. These are typically used for the classes in the Javascript files.
5. Search the files for any occurrences of <!-- {% raw %} -->`boilerplate`<!-- {% endraw %} --> (case-sensitive) and replace those with a lowercase machine-safe version of your system name, such as <!-- {% raw %} -->`mysystemname`<!-- {% endraw %} -->.
6. If the replace instructions from step 4 also included updating your description in system.json, you should edit that to be more readable now, such as "My System Name".

## Option 2:  Generate with npm

You'll need to be comfortable with your terminal/command line and have npm installed. If you are, run the following two commands:

<!--- {% raw %} --->

```bash
npm install -g yo
npm install -g generator-foundry
```

<!--- {% endraw %} --->

After that, you just need to open your <!-- {% raw %} -->`/Data/systems`<!-- {% endraw %} --> directory in your Foundry userData folder in your terminal and run

<!--- {% raw %} --->

```bash
yo foundry
```

<!--- {% endraw %} --->
to generate your system. The generator will ask you what your system name should be and will provide examples.


From here, you can skip to the next page or keep reading if you'd like to read about the other options for starting a new system.

## Other options

If you'd like to see other options for getting started with building a new system to start from, see the [Other options](https://foundry-vtt-community.github.io/wiki/SD01.2-Other-options) page.

---

* **Next**: [Stuff to be aware of](https://foundry-vtt-community.github.io/wiki/SD02-Stuff-to-be-aware-of)