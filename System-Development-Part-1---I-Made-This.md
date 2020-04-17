
![](https://lh4.googleusercontent.com/zFN4vx-WBA7LcxtHrhor6KUD68PMIh1S28FFrh07M59gAmSwaP8ClpZeRkBWeK7p8iu-OZHcdMPGXLaESYP0Te9qcluY55gNVZgujuTn5oB4KvqQLHnJyfoyA1kDC18s8w0mHVPa)

[https://nedroid.com](https://nedroid.com)

So first we need to create a system and have Foundry recognize that it’s a new game system (at least as far as we’re concerned.) We can save ourselves a lot of work by cloning an existing game system, fortunately Atropos was kind enough to have created one we can unashamedly steal and use for our own nefarious purposes.

  

1a. Install or download [Simple Worldbuilding System](https://gitlab.com/foundrynet/worldbuilding)

  

1b. Create a copy of the worldbuilding system in a new folder and name that folder with the following restrictions:

-   folder name is all lower case
    
-   folder name has no special characters or symbols
    
-   folder name contains no spaces
    

  

1c. Once you have done that, we’re going to open your new folder in your IDE of choice.

  

1d. Open the system.json file and change the values to suit your needs. We’ll want to make sure that:

-   “name”: “yoursystemname” - matches the folder name of your new system exactly
    
-   All other relevant data is completed in this list
    
-   We credit Atropos in our description. We are stealing his code after all.
    

-   “description”: “A rudimentary implementation of <yoursystemhere> for Foundry VTT, based entirely on the Simple Worldbuilding System for Foundry designed by Atropos.”
    

-   Note: if you aren’t intending to distribute this system (or at least not yet) you can leave url, manifest, and download as a ‘blank string’ (empty quotations).
    

  

1e. CHECK YOUR WORK! Open foundry (or restart it completely). If everything was right, Foundry will show a new system is installed. Common errors at this stage include not formatting the json correctly, the most likely one is putting an extra comma in the last entry of the file.

  

1f. Since we’re already here, let’s create a development world for our system so we can break stuff without risking anything, because oh boy are we gonna break stuff. Create a world called (DEV) - mygamesystemhere