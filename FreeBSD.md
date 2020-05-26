Download the Linux version of Foundry and place it in a suitable location, such as **~/FoundryVTT**. Extract the contents (you may need to install zip using `pkg install zip`). The zip does not contain a top-level directory, so be sure you extract into an empty directory.

In order to run the Foundry server we need to install `node.js`. In a terminal run `pkg install node`.

With `node.js` installed we can now run the Foundry server. Assuming you placed and named the extracted Foundry folder in your home directory and named it **FoundryVTT** you can type the following command replacing the folder names if needed
```
cd ~/FoundryVTT
```
Press the `return` key.

Now that we are inside the Foundry folder we can run the Foundry server by running this command
```
node resources/app/main.js
```
Press the `return` key.

You should now see something similar to this in your terminal
```
Foundry VTT | 2019-10-22 09:00:40 | [info] Foundry Virtual Tabletop - Version 0.3.8
Foundry VTT | 2019-10-22 09:00:40 | [info] Application Options:
{
  "port": 30000,
  "fullscreen": false,
  "isElectron": false,
  "isNode": true,
  "isSSL": false,
  "world": null,
  "background": false,
  "debug": false,
  "demo": false
}
Foundry VTT | 2019-10-22 09:00:40 | [info] Requesting UPnP port forwarding to destination 30000
Foundry VTT | 2019-10-22 09:00:40 | [info] Server started and listening on port 30000
```

With the Foundry server running you can now access it via your browser by typing `localhost:30000` in the URL bar.

To shut the Foundry server down press both the `control` + `c` keys at the same time with the terminal in focus.

You can save on some disk space by deleting the Linux-specific binary files.  You can delete the unneeded ones with the following command:

<!--- {% raw %} --->
```
rm -rf chrome* *.dat *.so locales *.bin *.pak swiftshader
```
<!--- {% endraw %} --->