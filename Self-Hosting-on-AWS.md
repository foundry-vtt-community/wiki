# Self-Hosting on AWS
## 1. Introduction, Requirements, and A Disclaimer

While the official KB provides some useful information for setting up Foundry VTT on AWS, a complete guide to doing so is outside its scope.  However, a guide to doing so that also outlines some best practices for the use of Amazon Web Services seems like it would be handy to help others along and make their setup process a little smoother.  This guide is intended as an outline of the basic infrastructure needed and how to set it up on AWS.  It is not intended as a guide for setting up and configuring the server itself.  The excellent Ubuntu setup guide [here](https://github.com/foundry-vtt-community/wiki/wiki/Ubuntu-VM) more than adequately documents how to set up the actual webserver and Foundry server.  I'll relink it again at the appropriate point in this guide, but you might want to keep it open in a separate tab.  Also, while this guide is intended to be approachable by people with little to no experience with the AWS platform, it is not intended as a general introduction to it.

I personally selected AWS in particular because it offers a very robust cloud hosting platform with a deep list of options and services at a competitive price.  Additionally, for those who haven't used AWS before, they offer new accounts [a number of services free for the first year](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc), which covers most of the expense of self-hosting Foundry in the cloud, and the fees for hosting are nominal thereafter.  AWS is by default pay as you go for all services, and only a certain level of usage is covered under the free tier.  If you are concerned about the potential charges involved, I highly suggest setting up a [billing alert](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html) using AWS Cloudwatch after setting everything up.  Amazon will automatically notify you when it projects you'll go over your limits.  Do note that as the author of this guide, I do not take responsibility for any overage charges accidentally incurred.  I will do my best to keep everything within the free tier, however.

Requirements for this guide are a web browser, a notepad app, and possibly some patience.  The Ubuntu server setup guide requires an SSH client and some familiarity with the Linux command line.

## 2. Setting up an AWS Account

If you already have an AWS account, please feel free to skip this section.  Everyone else, the first thing you'll need is an AWS account -- go to[aws.amazon.com](https://aws.amazon.com) and click the Create an AWS Account button in the top right.  Fill out the forms as listed, setting up a Personal account.  Do note that when it asks you for a payment method, you _must_ provide a valid payment method.  Even on the free tier, they will test the card with a nominal $1 charge to test to see if it's valid.  This charge will be credited back to your account after 3-5 days.  When they ask you to select a support plan, pick Basic, and you're done.  After you receive confirmation via email that the account is set up, you can log into the console and proceed.

## 3. Identity and Access Management (IAM), Part 1

Now that we have created an AWS account, we're going to create a couple of sub-accounts for the actual setup and management.  When you set up your AWS account, you created what they call a "root account", which has the keys to the entire castle.  Ideally, you'd use a less privileged account for the actual day to day tasks.

We're going to set up two accounts:
* An admin account to set up and manage the services we'll be using.
* A system account to let Foundry VTT access an S3 bucket for static hosting and object storage.

Locate the Services menu at the top of the AWS console.

<2-1 goes here>

Then on the menu that drops down, select IAM.

<2-11 goes here>

You should see the main page for AWS Identity and Access Management (IAM) come up.

<2-2 goes here>

Right now we're most concerned about the Users link on the left.  Click it and an empty user list will come up.  First, we're going to set up the admin user.  Click Add User at the top, and fill out the form that comes up.

<2-3 goes here>

You can set the user name to whatever you'd like -- I put admin here for simplicity's sake.  This user doesn't need a programmatic access key, so select AWS Management Console access only, and set them up with a custom password.  Uncheck Require password reset as you don't need to reset a password only you should know.  Click Next to get the set permissions dialog.

<2-4 goes here>

I've selected Attach existing policies directly and selected AdministratorAccess.  This will allow your admin account to manage all AWS services.  In a real world environment, we would want to be more picky on permissions, but this will do for this guide.  Hit Next to go to the Tags page, then Next to review the account, then Create User.  Hit Close in the bottom right after you're done.

<2-5 goes here>

Now that you have an admin account set up, let's create a user that Foundry will use to access assets on S3.  Follow the same Add User process again, but this time give the user a name like "foundry-s3-user".  Instead of giving them Console access, give them Programmatic Access.  Don't attach any policies, and click through to the final screen.  On step 5, you'll have the option to download a CSV file -- this contains the credentials that Foundry will use.  Download it, but keep it somewhere safe.

<2-6 goes here>

Our users are now set up.  We'll revisit the foundry-s3-user in a later step to grant them actual access to S3, but we need to set up the S3 bucket before we can do that.  Before we leave the first part of IAM setup, there's a couple more things we need to do.  Click the Dashboard link on the left to go back to the main dashboard.

<2-7 goes here>

At the top, I'd recommend clicking Customize by the IAM users sign-in link and giving the account an easy to remember name.  This will make it easier to log in as the admin user.  The name has to be globally unique, but once you've set a friendlier name, you'll get a link you can copy and paste into a bookmark.  Additionally, the checklist under Security Status is AWS' recommended ways to secure your account.  At the very least, I suggest activating multi-factor authentication (MFA) on the root account.  Google Authenticator and Authy are both good MFA apps available for all major smartphones.  Once you log in with the admin account, you can come back to IAM to set up MFA for that user as well, and I recommend doing so.

Now that you have a customized signin link and a separate admin user, open up a new tab, paste in your signin link, and log in under the admin account.

## 4. Elastic Cloud Compute (EC2)

On the same services menu you used to get to IAM, you'll note that EC2 is in the top left corner.  This is because it is far and away Amazon Web Services' most heavily used service.  It provides access to the setup and maintenance interface for the virtual private servers that put AWS on the map.  This setup guide will be using screenshots from the New EC2 Experience control panel.  If you toggle it off, things won't look exactly the same, but the same options should still be roughly available.  However, as this is probably the most complex part of the infrastructure setup, I advise toggling on the New EC2 Experience for clarity's sake.  

Before we get started, I need to introduce a basic concept: AWS regions.  All AWS resources launch in a given region, usually indicated by a locale code, then what side of the locale it's in, and then the number of the region on that side of the country.  For instance, AWS' Oregon data centers fall under US-West-2, while their Dublin data centers are EU-West-1.  You can see what region you're in at the top right of any AWS dashboard.  I suggest using one that's close to all of your players, to minimize latency.

On the left hand toolbar, click on Instances.  You should see the following screen.

<3-1>

Click on either of the Launch Instances button.  That'll take you to the page for selecting the AMI you want to launch.  AMIs are base templates for instances -- they provide the OS install and a preselected software package.  In this case, the Ubuntu 18.04 image will just come with Ubuntu and an assortment of must-have utilities.

<3-2>

For this guide, we'll be using the Ubuntu Server 18.04 LTS (HVM), SSD Volume Type AMI.  Leave it on the default of 64-bit (x86), and hit Select.  The next screen will let you choose the type of instance you want to use.  It should default to t2.micro, which is reasonable for a Foundry server.  Also, as the little label by the type will mention, it's eligible for free tier, which no other instance type is.  Hit Next: Configure Instance Details.

<3-3>

I have not included the full list as you can ignore most of them.  Just make sure Number of instances is set to 1, and Auto-Assign Public IP is set to Use Subnet Setting (Enable) or Enable.  Your instance will need a public IP to be accessible from the wider internet.  The rest is a fairly reasonable set of defaults.  Click Next: Add Storage.

<3-4>

This set of defaults is perfectly reasonable, as we will not be storing the game assets on the instance itself.   Ubuntu 18.04 Server and Foundry, along with all the required dependencies, take up about 2.2gb installed. Storage-heavy data like images will get pushed to S3, which is generally cheaper for storage and serving them up after the free tier benefits end.  If you'd prefer on-instance asset storage, you can provision this with as much space as you think you'll need and use the standard local storage options in Foundry.  However, do note that the charge for EBS space is higher, per gigabyte-hour, than S3.

Once you've settled on how to handle your storage, click Next: Add Tags.  You can add any tags you might want in key-value pairs here, but none are required.  Tags are generally handy if you're running a number of different servers tasked with different things, so you might want to at least set a Name tag for your instance, but again, it's not required.  Click Next: Configure Security Group.

<3-5>

This is where you're going to set up the traffic allowed through to your instance.  By default, your instance will permit SSH traffic for management from anywhere.  You can make this more secure by clicking on the dropdown that says Anywhere, and changing it to My IP.  AWS will automatically pull the public source IP for your traffic and restrict SSH traffic to that IP only.  Please note that most residential ISPs do dynamic public IP addressing, so you are not guaranteed to have the same address day to day -- if SSH login works one day, but not the next, you'll need to edit the security group later.  Click Add Rule twice and add rules for HTTP and HTTPS traffic at a minimum.  You may also need to allow additional ports through for voice and video traffic -- I'd advise referring to the guides for those to get the appropriate port ranges.

You can edit security groups at any time via the EC2 control panel, and changes are instant, so don't feel you have to get things perfect right now.  SSH, HTTP, and HTTPS are the minimums required to setup Foundry and verify it's working.  Click Review and Launch when you're ready to move on.  This will bring you to the last page, which lets you review your instance setup.  There is one final task to do before the instance is launched.  Click Launch, and this window should pop up.

<3-6>

By default, EC2 uses key pairs to regulate access.  Select Create a new key pair, give it a name, and hit download.  Save it somewhere safe where you will remember it.  I cannot emphasize this strongly enough: _if you lose this file, you will not be able to log into your instance.  The instance will need to be recreated -- no one, not even AWS Support, can recover a lost private key._

Hit Launch, wait while the spinner spins, then hit View Instances once you get the Launch Status page.  A new instance can take a few minutes to go from zero to hero, so go get a glass of water and come back.  Refresh the page, and it should show as running and passing the status checks.  Highlight it if it isn't already, and get the IPv4 Public IP out of the information at the bottom.  Copy-paste that to a notepad, we'll need that later.

## 5. Simple Storage Service (S3)

If EC2 is what runs everything on AWS, S3 is what stores it (mostly).  The service mostly lives up to its name, as it provides an easy way to store large amounts of objects.  These objects can be, so far as we're concerned for this, of basically unlimited size -- sending more than 5gb in a single file requires special transfer methods, but other than that, as long as you're willing to pay per gigabyte-hour for it to get stored, they'll host it.  Open the Services menu and click on S3 near the top left.

<4-1>

This is the basic S3 console.  Hit Create Bucket.

<4-2>

The bucket name needs to follow a certain set of conventions.  First, it can only contain lowercase letters, numbers, and dashes.  Second it must be _globally_ unique across _all_ AWS regions and accounts -- for example, if I create a bucket called foundry-vtt-assets, you cannot create a bucket with the same name, even though we're using separate accounts.  Leave the region on the default.  Under Bucket settings for Block Public Access, uncheck Block _all_ public access and acknowledge the risk.

Normally, I would not use this setting, but Foundry requires that the bucket be made public as it links players directly to assets in the bucket.  If the bucket isn't public, the links won't work.  Hit Create Bucket.

When you go back to the dashboard, you should see the new bucket there.  Click on the little circle to the left of the name and click Copy ARN above it.  Paste that into a notepad -- we'll need it in the next section.  Click on the bucket name after you've got the ARN.

<4-3>

This is the bucket itself.  Click on the Permissions Tab, then click on CORS configuration.  The Foundry defaults for bucket setup can be found [here](https://foundryvtt.com/article/aws-s3/).  I suggest just copy-pasting the CORS configuration on that page in and hitting save.

That's it for bucket setup.  Now all we have to do is set up our system account to have permissions to access only this bucket.

## 6. IAM, pt. 2

We need to set up a custom policy that locks down the user we set up for Foundry to access S3 and allows them to only access Foundry-related assets.  If this is the first time you've used AWS, it may not seem like it's necessary at this point, but if you start using it for more and more tasks, you'll come to appreciate restricting accounts access to anything they don't need.  First we need to set up a custom permissions policy.  Click Policies on the left, then click Create Policy.  This will bring up the Policy Editor.

<5-1>

Click the JSON tab, delete the text already in the field, and paste in the following policy:

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": [
                    "s3:PutObject",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:DeleteObject",
                    "s3:PutObjectAcl"
                ],
                "Resource": [
                    "arn:aws:s3:::(my-bucket)/*",
                    "arn:aws:s3:::(my-bucket)"
                ]
            },
            {
                "Sid": "VisualEditor1",
                "Effect": "Allow",
                "Action": "s3:ListAllMyBuckets",
                "Resource": "*"
            }
        ]
    }

Hit Review and give it a name that's easy to find -- like foundry-s3-access-policy.  Next, click Users on the left hand side, then click on the name of your Foundry S3 user.  You'll see a large button asking you to add permissions to the account, as it does not currently have any.  This will bring up the Grant permissions dialog.

<5-2>

Click the Attach existing policies directly button.  This will bring up a long list of Amazon-made permissions policies, but you can use the search bar at the top to bring up the policy we just made by searching for its name.  Click the checkbox by it, and hit Next: Review, then Add Permissions.

## 7. Server Setup

You're now ready to set up your new AWS-hosted Ubuntu server with Foundry.  Again, you can find the generic guide [here](https://github.com/foundry-vtt-community/wiki/wiki/Ubuntu-VM).

You'll need the key pair you created in order to log in via ssh.  A typical command to log into an EC2 at a command line:

    ssh -i path/to/keypair.pem ubuntu@<your-instance-public-ip>

This should work in both a Linux or MacOS terminal, or in Microsoft Powershell on most modern installs of Windows 10.

After you've set up Foundry, you'll want to go back to the Foundry S3 setup [here](https://foundryvtt.com/article/aws-s3/) and make the appropriate edits to the options.json file, and create a aws.json file with the appropriate access key and private key, as well as the region.  The keys are in the .csv file you made all the way back in IAM, part 1.  The region is the AWS-compliant name of the region your bucket is located in -- if you hit the Regions dropdown in the top right, it'll be in all lower case next to the friendlier name.

## 7. Final Notes

Like most pieces of documentation, this is a living document.  If you run into any issues with the instructions here, please reach out to me.  I am @magichateball on the Foundry VTT Discord and will do my best to field any questions you have related to these instructions.