## Solution 1 : Dual computers

Of course, local play can be achieved with 2 (or more computers). In the 2 computers settings, 1 computer is dedicated to the GM, and the other one to show the scene/maps/etc. to the players.
To do this, create a specific 'IRL' player with the 'Observer' role for all the PCs.

## Solution 2 : Single laptop ( VM solution)

This solution is using a VM (Virtual Machine) to handle the player session, hence it works with Linux, Windows and probably Mac.

Hardware setting : 

* One laptop, used by the GM
* One screen, connected to the laptop, and oriented to the players

Software setting :

* One VM hypervisor of your choice (VMWare, KVM, Proxmox, Virtualbox). Note that VMware should be prefered, as the sharing of the GPU is more easy to setup with this tool.
* On VM, running in the hypervisor, with Chrome installed. I selected Lubuntu 20.04, because its light and fast, but you can choose the OS of your choice, of course.
* Inside the Guest OS, attach a USB mouse (ie detaching from host), in order for the players to navigate in the scenes/maps on their own.

Running :

* Launch Foundry and connect to it with your browser (laptop GM side)
* Launch the guest OS in the VM
* In the guest OS, launch Chrome and connect to FOundry using the observer player created previously
* Setup fullscreen and provide the VM attached mouse to the players 
* Play !

Main source (in French)  : http://www.lahiette.com/leratierbretonnien/foundryvtt-pour-table-reelle/

## Solution 3 : Single laptop, dual mouse pointers (Linux only)

If you are using Linux, another solution exists, without the need of a VM, by creating 2 independant mouse pointers (and even keyboards if you want).

The hardware setup is the same than oin solution 2 above.

The software setup is a bit different : 

* Connect as root
* Create a second pointer with : `xinput create-master aux`
* Connect a second mouse (USB preferably) to your computer
* List the available input devices with : `xinput list`
* From this list, get the id of the new mouse, and the id of the 'aux' pointer
* Enter the command : `xinput reattach <mouse-id> <aux-id>`
* You now have 2 pointers, moving indepently !
* Then launch your GM session in a Chrome instance
* And the players session in a second Chrome instance, launched in "privacy" mode.
* Moves the Chrome windows to the relevant screens
* Play !

Main source (in French)  : http://www.lahiette.com/leratierbretonnien/foundryvtt-pour-table-reelle/
