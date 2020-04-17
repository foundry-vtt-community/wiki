
![](https://lh3.googleusercontent.com/qoT-9iXu-1UwimiVSs-q6a9uDc7jN0aUBknVi7d7hHV3r37VOIQ1jFuCrE0tcWXLWlYPzs5yY404GsmTIEWyce-iqFVJf-ZQbySI_pa9al1fBmw_TFzVXcHQA8NMnbdHmOqcs-OT)

  
What follows is the monotonous part where we enter data into our template.json for each and every attribute, stat, ability, skill, or anything we want to be represented in a set of data. This doesn’t need  to be done all at once; we can come back and add to it at any time. However, there are a few things we should keep in mind about editing this data:

  

-   Any changes we make in the template.json don’t take effect for Foundry until after we save the template.json and restart Foundry. Refreshing or using F5 will not be sufficient.
    
-   Anything we delete will remain in the records of old actors but not be created for new actors.
    
-   Anything we add will not be added to existing actors, only new ones we create (except if we trigger a data migration; more on that later).
    

  

## 4a. Putting Stuff Back

Remember back in part 3c when I had you delete the line from your template.json that read: 

    ,
    
    "attributes": {}
    
    }

  

Well. We didn’t actually have to do that- so let’s put it back, and while we’re at it, let’s add some skills:

  
  

Before

![](https://lh6.googleusercontent.com/KJCYcNfvl859zAsV93ds5Ss3sDDdFh8i8e7YwCqJGjsqUUzrVmqTd1qPyStHEKevP2n__mIzJmnA2hA3QR5ocmAcDISx1HNPXblr6pRQdC1hsXQCRnuoUhy_hpcrtXquILxStd_H)

  
  
  
  
  

After

![](https://lh3.googleusercontent.com/i3sGXerU1cMTA2LFkxmhxzsMYiO1079rPUOxk0k_PtG7JbslE5dJmZLK-mawdZQeSXaGEDNki3BneWFRYP0dyhfP4FKbLTwhe8DGFJfJMnn7PC197pvsPbSYIRgQSSakTwK0Kgjd)  

Here’s where we get to really start padding out those JSON lines.

  

## 4b. Syntax isn’t something you pay for cigarettes and liquor

A suggested format for new attributes and skills, you can change any name here, even attributes or skills:

    "attributes": {
    
    "strength": {
    
    "value": 0,
    
    "label": "Strength",
    
    "modifier": []
    
    }
    
    },  
    "skills": {
    
    ...
    
    }
    
      

The “modifier”: [] entry is WHOLLY optional, but can be used later to add modifiers to those attributes and skills if you get clever with javascript. There really isn’t a downside to including it here.

  

Start pumping out those character stats, friend.

  

4c. Really, just keep making entries here until you run out of things on your character sheet you need to record and store data for. When you think you’re done, save your template.json and we can move on to creating that sheet.