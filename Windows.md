# Hamachi

Hamachi is a really simple tool which allows you to create a virtual private network which simulates a LAN-type connection that allows other people to connect to you as an alternative if you are unable to port forward. You can download it [here.](https://www.vpn.net)

After installing it it will prompt you to create an account so sort out such formalities.

After that you will be met with this little screen. 

![](https://i.imgur.com/vEU4Y4r.png)

## Hosting

To host your own server it's really simple. Network > Create a New Network

![](https://i.imgur.com/u6goQvT.png)

Make sure to write down and memorize the servers ID and password, this will be used so that other people can connect to your server.

![](https://i.imgur.com/Nbj01XK.png)

## Joining

Network > Join an existing network

![](https://i.imgur.com/t8SQrPm.png)

Enter the servers ID and Password and you are in!

![](https://i.imgur.com/mGA7tSN.png)

To connect to FVTT all you need is the IpV4 address of the host.

![](https://imgur.com/4ukq4px) 

In my case it's 25.70.36.41:30000.

To get it manually Right Click on the host > Copy IpV4

![](https://i.imgur.com/2KobBh9.png)

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

