# Basic Setup
1. Download the latest Windows setup file from [Patreon](https://patreon.com/foundryvtt/posts)
2. Run `FoundryVTT-0.4.0-Setup.exe` to install Foundry VTT (note: your version might not show 0.4.0)
Note: If you are running Windows 10 you may see the following warning:    
![https://i.imgur.com/aTfmxeq.png](https://i.imgur.com/aTfmxeq.png)    
Click More Info, then Run Anyway:    
![https://i.imgur.com/nBjS6J6.png](https://i.imgur.com/nBjS6J6.png)    
3. Follow the instructions to install Foundry.
Note: If you select Run Foundry VTT at the end of installation you may be prompted to allow it through your Windows firewall. Click Allow:     
![https://i.imgur.com/Q5FMI1O.png](https://i.imgur.com/Q5FMI1O.png)    
4. If you see this screen you have successfully installed Foundry VTT:    
![https://i.imgur.com/CnGbXAK.jpg](https://i.imgur.com/CnGbXAK.jpg)    

If you need to launch Foundry again (for example you reboot your PC), you will can run `FoundryVTT.exe` from the folder you installed Foundry VTT in, or you can click the link in the Start Menu or Desktop.

# Hamachi

Hamachi is a really simple tool which allows you to create a virtual private network which simulates a LAN-type connection that allows other people to connect to you as an alternative if you are unable to port forward. You can download it [here.](https://www.vpn.net)

After installing it it will prompt you to create an account so sort out such formalities.

After that you will be met with this little screen. 

## Hosting

To host your own server it's really simple. Network > Create a New Network

Make sure to write down and memorize the servers ID and password, this will be used so that other people can connect to your server.

## Joining

Network > Join an existing network

Enter the servers ID and Password and you are in!

To connect to FVTT all you need is the IpV4 address of the host.

In my case it's 25.70.36.41:30000.

To get it manually Right Click on the host > Copy IpV4

# ZeroTier

If your party+GM is more than 5 people, you cannot use Hamachi without paying a subscription since it allows a network of 5 people maximum.
One good solution is ZeroTier.
These are the steps to create a virtual network and create your Foundry session.

For GMs
1.	Download Zerotier from https://www.zerotier.com/download/
2.	Install it
3.	Register yourself from https://my.zerotier.com/login. A free subscription is enough for our purpose.
4.	Once registered, go to https://my.zerotier.com/network and create a new network. Make it public.
5.	Once created, in the network properties you should have an alphanumeric network id (something like 0dddb752f775c1e2). Select and copy (Ctrl+c) it.
6.	In the system tray you should have this icon ![](https://i.imgur.com/gNesEDY.png) . Clicking on it will open a menu. Click on join a network and insert the network id copied at point 5. Click ok.
7.	Now your pc is in a virtual network. In the page https://my.zerotier.com/network/<networkid> at the section “Member” you should see your address (mac), your managed IPs, Last seen, Physical IP. Copy your Managed IPs

For each player:
1.	Download Zerotier from https://www.zerotier.com/download/
2.	Install it
3.	In the system tray you should have this icon ![](https://i.imgur.com/gNesEDY.png) . Clicking on it will open a menu. Click on join a network and insert the network id of your GM (point 5). Click ok. Now be sure there is something like this on your Zerotier tray:   

Now the GM must append :30000 to his ZeroTier Managed IP (see point 7 above). Voilà, this is the FVTT invitation link.

WARNING:
Zerotier installs on your pc as an automatic service. It means unless you set it as manual on you Services list it will run as soon as your OS is started, so you don't need to "run" it, unlike Hamachi. You are always connected to the vpn it creates.
