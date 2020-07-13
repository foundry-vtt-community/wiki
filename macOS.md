# Basic Setup
1. Download the latest Windows setup file from [Patreon](https://patreon.com/foundryvtt/posts)
2. Run `FoundryVTT-0.4.X-Setup.dmg` to install Foundry VTT.
Note: The .dmg is currently not signed, so you will need to allow the installation when prompted
 a. Go to System Preferences under the Apple icon in your system tray,
 b. Open Security & Privacy,
 c. If settings are locked, use administrator login credentials to unlock the settings by clicking the padlock icon at bottom,
 d. Click the "Open Anyway" button (may not be shown if you didn't try to open FoundryVTT right away after downloading), and choose Open in the next dialog box.  Finally, allow incoming connections in the next dialog.
3. Follow the instructions to install Foundry.
Note: If you select Run Foundry VTT at the end of installation you may be prompted to allow it through the macOS firewall.   
4. When finished installed Foundry will open as a full screen application on the "Foundry Virtual Tabletop - Configuration and Setup" screen.

# Running From Terminal

Download the Window's version of Foundry and place it in a suitable location, such as **Documents**. Double click on the `FoundryVirtualTabletop-win32-x64.zip` to extract the contents. I suggest renaming the folder that was created to **FoundryVTT**.

In order to run the Foundry server we need to download `node.js` for macOS. It is suggested to install `node.js` via [Homebrew](https://brew.sh/) for ease of installation and managment.

To install Homebrew, open up the **Terminal** application and copy the following command
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Press the `return` key.

During installation it will ask for a password, this is the password that used login to macOS. Once typed, press the `return` key.

Once complete you should see *Installation successful!*

With Homebrew installed we can now install `node.js` to do this enter the following command in **Terminal**
```
brew install node.js
```
Press the `return` key.

With `node.js` installed we can now run the Foundry server. Assuming you placed and named the extracted Foundry folder in your **Documents** and named it **FoundryVTT** you can type the following command replacing the folder names if needed
```
cd /Documents/FoundryVTT
```
Press the `return` key.

Now that we are inside the Foundry folder we can run the Foundry server by running this command
```
node resources/app/main.js
```
Press the `return` key.

Now depending on the version of macOS you may get a prompt to allow node to accept incoming network connections, press **Allow**.

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

To shut the Foundry server down press both the `control` + `c` keys at the same time with the **Terminal** application in focus.