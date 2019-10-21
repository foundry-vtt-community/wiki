Unpack the zip file in a suitable location, and then open the unpacked folder. Open a terminal window in this location and run the command:
`node resources/app/main.js`

You should now see a message saying VTT is running. 

Closing the terminal will stop the application.

For a server that runs without the need for a terminal or that restarts automatically at boot up, you should leverage a tool such as [`systemd`](https://www.freedesktop.org/wiki/Software/systemd/) or [`upstart`](http://upstart.ubuntu.com/).