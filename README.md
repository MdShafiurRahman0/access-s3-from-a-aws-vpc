# Access S3 from a AWS VPC


# Get ready to:

☁️ Set up a VPC with an EC2 instance.
🔑 Use access keys to give your EC2 instance the power to use your AWS account.
🪣 Interact with Amazon S3... through your EC2 instance!


#  High Level Overview of Project Architecture :

![image](https://github.com/user-attachments/assets/19213d11-7a8a-44bc-b0cc-268f14f19903)


# Step 1: Set up  VPC and EC2 Instance

![image](https://github.com/user-attachments/assets/670de0fd-f323-4a95-8ad8-67caba244922)



1. Select Create VPC.

2. Select VPC and more.

3. Under Name tag auto-generation, enter

4. The VPC's IPv4 CIDR block is already pre-filled to 10.0.0.0/16 - we'll use this default CIDR block!


![image](https://github.com/user-attachments/assets/1891a253-59c6-41db-9fba-e8b4e7342cc7)


5. For IPv6 CIDR block, we'll leave in the default option of No IPv6 CIDR block.

6. For Tenancy, we'll keep the selection of Default.

7. For Number of Availability Zones (AZs), we'll use just 1 Availability Zone.

8. Make sure the Number of public subnets chosen is 1.

9. For Number of private subnets, we'll keep thing simple today and go with 0 private subnets.

10. For the NAT gateways ($) option, make sure you've selected None. As the dollar sign suggests, NAT gateways cost money!

11. For the VPC endpoints option, select None.


![image](https://github.com/user-attachments/assets/73033c80-c66d-4d28-a41c-5658a9924a2d)


# Step 2:  Launch an instance in your VPC



1. Head to the EC2 console - search for in the search bar at the top of screen.

2. Select Instances at the left hand navigation bar.

3. Select Launch instances.

4. Since your first EC2 instance will be launched in your first VPC, let's name it 

![image](https://github.com/user-attachments/assets/c55fb036-56a0-4663-b67a-59ae0c83524a)


For the Amazon Machine Image, select Amazon Linux 2023 AMI.
For the Instance type, select t2.micro.
For the Key pair (login) panel, select  Proceed without a key pair (not recommended).
At the Network settings panel, select Edit at the right hand corner.
Under VPC, select NextWork-vpc.
Under Subnet, select your VPC's public subnet.
Keep the Auto-assign public IP setting to... do you remember whether our EC2 instance needs a public IP address?
💡 Hmmm, I can't seem to remember. What is it?
We're using EC2 Instance Connect after this to connect with our EC2 instance!

EC2 Instance Connect requires instances to be in a public subnet AND have a public IPv4 address!


💡 What is EC2 Instance Connect?
EC2 Instance Connect is an EC2 tool designed to help you get direct access to your EC2 instance!

Once you get direct access to your EC2 instance, you're going into the instance's terminal. This lets you do some advanced work like installing software into your EC2 instance or accessing another AWS service!

Select Enable.
Step 1: Your instance's network settings.
Step 1: Your instance's network settings.

For the Firewall (security groups) setting, choose Create security group.
⏸️ PAUSE
Before you read ahead - can you figure out the correct security group settings for this EC2 instance?

Hint: you WON'T need to run ping tests in this project!

Hmmm!
🤔
🤔
🤔

▶️ Alright - steps below!

Name your security group 
That's it! No security group rules to add.
💡 Didn't we use to add other security group rules?
By default, this new security group allows all inbound SSH traffic. That's all we need to use EC2 Instance Connect later.

We used to add an inbound rule to allow ICMP traffic - but we won't need it if we aren't running any ping tests!

Step 1: Your new security group settings.
Step 1: Your new security group settings.

Select Launch instance.
✍️ What resources did you launch in this step?
Start your response with 'I started my project by launching'...

Go on, we know you have a great answer..

250 characters left

Gray check icon


💻 Step #2
Connect to Your EC2 Instance

In this step, we're gonna connect to your EC2 instance and try access an AWS service!



In this step, you're going to:

Connect directly to your EC2 instance.
Step 2: Connect to your EC2 instance
Step 2: Connect to your EC2 instance

✍️ What are we doing in this step?
In your own words, start this step by explaining what you're about to do and why.

Go on, we know you have a great answer..

250 characters left

Gray check icon


Head to your EC2 console and the Instances page.
Select the checkbox next to Instance - NextWork VPC Project.
Select Connect.
In the EC2 Instance Connect set up page, select Connect again.
Yay! Successfully connected.
Step 2: Feels good that we've connected right away!
Step 2: Feels good that we've connected right away!

For your first command, try running 
, which is a command used to list the S3 buckets in your account (yup, ls stands for list!).
💡 Wait, you can view S3 buckets from an instance's terminal?!
Yes, you can! From an EC2 instance's terminal, you can run all kinds of commands to interact with AWS services. Listing all the S3 buckets you have access to is just the tip of the iceberg!


💡 How does that work?
There is a special software called the AWS CLI (Command Line Interface) that you install and run on your computer to control AWS services directly from the command line i.e. your terminal! You can install this in your local computer too, and all EC2 instances come with it already installed.


Extra for Experts: As you advance in your cloud engineering career, you'll find that the AWS CLI often becomes your go-to tool. Engineers use the CLI to automate tasks and manage AWS resources efficiently using scripts, making it essential for managing your cloud environment in an efficient way.

While the AWS Management Console is fantastic for learning and having a visual guide, the CLI provides the speed and versatility that professionals need for complex tasks.

Step 2: Run `aws s3 ls`
Step 2: Run `aws s3 ls`

Hmmm, doesn't look like a success. We need to provide credentials.
💡 What are credentials?
Credentials in AWS are like keys that let you access and manage AWS services securely. Without credentials, you won't have the permission to do things like viewing your S3 bucket list.


💡 Do I have credentials?
When you log into your AWS Management Console, you're already authenticated using your AWS user's details.

Running commands from an EC2 instance is a different story! You can think of your EC2 instance as another user that needs its own username and password (i.e. credentials) to get access to your AWS account.

Your account by default doesn't have credentials set up for running commands from an EC2 instance. You'll need to manually set these up to securely access and manage AWS services from your instance.

Run 
The terminal is now asking us for an Access Key ID!
Step 2: Run `aws configure`
Step 2: Run `aws configure`

💡 What is an access key ID? Do I have one?
An access key ID is a part of a credential!

Your credentials are made up of a username and password; think of the access key ID as the username.

You don't automatically have one, but you can create access keys IDs through AWS IAM.


💡 What's the difference between access keys and key pairs?
You might remember key pairs from launching EC2 instances!

Key pairs are used specifically for logging into your EC2 instances through SSH.

Access keys, which are what we're learning about now, are credentials for your applications and other servers to log into AWS and talk to your AWS services/resources.

Take a screenshot 📸
Take a screenshot of your terminal showing the two commands you ran!





Gray check icon


🔑 Step #3
Create Access Keys

Challenge accepted! Your EC2 instance needs credentials to access your AWS services, so let's set up access keys right away 🏃‍♀️



In this step, you're going to:

Give your EC2 instance access to your AWS environment.
Step 3: Create access keys.
Step 3: Create access keys.

✍️ What are we doing in this step?
In your own words, start this step by explaining what you're about to do and why.

Go on, we know you have a great answer..

250 characters left

Gray check icon


Search for 
 in the search bar.
Aha! So it's the IAM console that helps us set this up. Select IAM.
Step 3: Head to the IAM console.
Step 3: Head to the IAM console.

Search for 
 again in the IAM console's left hand navigation panel.
Step 3: Search for `Access keys` one more time.
Step 3: Search for `Access keys` one more time.

Choose the search result for managing an access key for your IAM Admin account.
Step 3: Choose the search result that mentions your IAM user name.
Step 3: Choose the search result that mentions your IAM user name.

Select Create access key.
On the first set up page, select Command Line Interface (CLI).
Select the checkbox that says I understand the above recommendation and want to proceed to create an access key.
Step 3: Set up your access key.
Step 3: Set up your access key.

✍️ What is the best practice alternative to using access keys?
Start your response with 'Although I'm using access keys in this project, a best practice alternative is to use'...

Go on, we know you have a great answer..

250 characters left

Gray check icon


💡 What is the yellow warning banner saying?
In this project we're creating access keys and manually applying them in our EC2 instance, but typically the recommended way is to create an IAM role with the necessary permissions and then attaching that role to your EC2 instance.

Your EC2 instance would inherit the permissions from the role, and this is best practise as you can easily attach and detach EC2 instances from roles to give and take away their credentials.

We aren't using this method so that we can learn about access keys, but roles are usually a better alternative for security.


💡 Extra for Experts: What do the other options mean?
Let's break 'em down!

Choose Local code if you're building an application in your local computer, and need the access key to connect your app with AWS services.
Choose Application running on an AWS compute service if you're building an application that's running on an AWS compute service like EC2 or Lambda, and need the access key to connect your app with AWS services.
Choose Third-party service if you're running an application from an external company (i.e. it wasn't built by yourself or AWS), but requires access to your AWS environment. For example, Crowdstrike is a third party security service that requires access to your AWS environment to protect them in real time!
Choose Application running outside AWS if you're running an application built by yourself but hosted on a physical server or another cloud platform, and you need to integrate it with AWS services.
Select Next.
For the Description tag value, we'll write 
Step 3: Give your access key a description.
Step 3: Give your access key a description.

Select Create access key.
OOoo this is important! STAY ON THIS PAGE ✋
Step 3: Stay on this page!
Step 3: Stay on this page!

You've just created your access key, well done.

This is the only time that your secret access key can be viewed or downloaded. You cannot recover it later. However, you can create a new access key any time.

💡 What is the secret access key?
The secret access key is like the password that pairs with your access key ID (your username). You need both to access AWS services.

Secret is a key word here - anyone who has it can access your AWS account, so we need to keep this away from anyone else!

Select Download .csv file near the bottom of the page.
🚨 PLEASE don't forget to delete your access key and the .csv file at the END of your session!

If you don't finish this project today, it's better to delete your access key and create a new one tomorrow, than to keep the same access key for a longer period of time.

✍️ What is a secret access key?
Start your response with 'Secret access keys are'...

Go on, we know you have a great answer..

250 characters left

Gray check icon


🪣 Step #4
Create an S3 bucket with 2 files

Access keys DONE.

Before we jump back into our EC2 instance, let's create a bucket in Amazon S3 🪄

After creating this bucket, we'll learn how to access it from our EC2 instance and do things like checking what objects are in the bucket.



In this step, you're going to:

Launch a bucket in Amazon S3.
Step 4: Create an S3 bucket.
Step 4: Create an S3 bucket.

✍️ What are we doing in this step?
In your own words, start this step by explaining what you're about to do and why.

Go on, we know you have a great answer..

250 characters left

Gray check icon


Search for S3 at the search bar at the top of your console.
Step 4: Search for S3 at the search bar up top.
Step 4: Search for S3 at the search bar up top.

Make sure you're in the same Region as your NextWork VPC!
Select Create bucket.
Step 4: Select Create bucket - here we goooo.
Step 4: Select Create bucket - here we goooo.

Let's set up your bucket! Keep the Bucket type as General purpose.

Your bucket name should be 

Don't forget to replace yourname with your first name! S3 bucket names need to be globally unique.
We'll leave all other default settings, go straight to Create bucket.



Nice! Bucket created 😎 😎

Step 4: Bucket created! That was fast.
Step 4: Bucket created! That was fast.

Next, let's upload two files into the bucket.

This can be any two files in your local computer!

Click into your bucket.
Select Upload.
Step 4: Select Upload.
Step 4: Select Upload.

Select Add files in the Files and folders panel.
Step 4: Select Add files.
Step 4: Select Add files.

Select two files in your local computer to upload.



Not sure what to upload? You can download and use these images instead! 👇

Right click on each link, select Save link as... and select Save.

NextWork - Denzel is awesome.png
NextWork - Lelo is awesome.png



Your files should show up in your Files and folders panel once they're uploaded!

Step 4: What Files and folders will look like after uploading.
Step 4: What Files and folders will look like after uploading.

Select Upload at the bottom of the page.
Take a screenshot 📸
Take a screenshot of your Objects tab showing two new files!





Gray check icon


🔌 Step #5
Connect to your S3 bucket

S3 bucket created 🪣✨

Shall we try use our EC2 instance to interact with it? 👀



In this step, you're going to:

Head back to your EC2 instance.
Get your EC2 instance to interact with your S3 bucket.
Step 5: Connect to your S3 bucket.
Step 5: Connect to your S3 bucket.

✍️ What are we doing in this step?
In your own words, start this step by explaining what you're about to do and why.

Go on, we know you have a great answer..

250 characters left

Gray check icon


Now back to your EC2 Instance Connect tab!
Are you ready to enter your Access keys details now?
Open the AccessKeys.csv file you've downloaded.
Copy the Access key ID.
Paste this into your EC2 instance's terminal, and press Enter on your keyboard.
Step 5: Enter your Access key ID.
Step 5: Enter your Access key ID.

Let's do the same for the AWS Secret Access Key!
Copy the key from your .csv file, and paste it in the terminal. Press Enter.
Next, for your Default region name, open your Region dropdown on the top right hand corner of your AWS console.
Copy your Region's code name. For example, us-west-2.
Step 5: Copy the Region's code name.
Step 5: Copy the Region's code name.

Paste that in your EC2 instance's terminal. Press Enter on your keyboard.
We don't have a default output format, so we can leave that empty. Press Enter.
💡 What is a default output format?
In just a second, you'll be running a few CLI commands in your EC2 instance's terminal to use Amazon S3. The default output format is how the results of your commands will display!

Options for your output format options are...

, which is the default if you're not using another option.
 for plain text.
 for an formatted table.
, which is a format for writing data in a way that is easy for people to read and write.

💡 What is JSON?
Amaaaazing question! JSON is a format for storing and exchanging data that is easy to understand for both humans and computers.

You'll get to use JSON and see it in action in a second 😎

Step 5: Leave the default output format empty.
Step 5: Leave the default output format empty.

Nice! Set up is done.
✍️ What was the purpose of the 'aws configure' command?
Start your response with 'To set up my EC2 instance to interact with my AWS environment, I configured'...

Go on, we know you have a great answer..

250 characters left

Gray check icon


Let's try running the 
 command again to see a list of your account's S3 buckets.



YOOOOOO look at that! Do you see a list of your buckets? You might have a shorter list than the one in this screenshot, but the only line to look out for is vpc-project-yourname.

Step 5: Do you see your bucket name?
Step 5: Do you see your bucket name?

Take a screenshot 📸
Take a screenshot of your terminal's response!





Gray check icon


Next, let's run the command 
. Make sure to replace 
 with your actual bucket name.

Based on the command, and what you've learnt about aws s3 ls, can you guess what this command does?

Nice - we can even see the objects that are inside your bucket!

Step 5: Oooo you can even peek at the objects inside your bucket.
Step 5: Oooo you can even peek at the objects inside your bucket.

Take a screenshot 📸
Take a screenshot of your terminal's response!





Gray check icon


Did you know you could upload files using AWS CLI too?!

Run 
 to create a blank .txt file in your EC2 instance.
💡 What does this command say?
Let's break it down!

sudo stands for "superuser do" and it's used when you're running a command that typicaly needs elevated user permissions, like installing software or creating new files.

touch is a standard command used to create an empty file if it doesn't exist. If it does exist, this command will update the file's timestamp (i.e. the last time it was accessed) instead.

/tmp/ is a common directory path (you can think of a directory path as layers and layers of folders) typically used for temporary files.

test.txt is the name of the empty file you're creating!

Next, run 
 to upload that file into your bucket.
💡 What does this command say?
Let's break it down!

aws s3 c: is the command to copy files.

/tmp/test.txt is the source file path. It's saying that the file to copy is test.txt, which exists inside a folder called tmp.

s3://nextwork-vpc-project-yourname is the destination path. It's saying that the file should be copied to the S3 bucket vpc-project-yourname!

Finally, run 
 again - what objects are listed in your bucket now?
Step 5: Run `aws s3 ls s3://nextwork-vpc-project-yourname` again.
Step 5: Run `aws s3 ls s3://nextwork-vpc-project-yourname` again.

💡 What is the 0 next to test.txt?
The numbers next to each file name is the size fo that file! Since test.txt is an empty file with no data, it has 0 bytes.

Take a screenshot 📸
Take a screenshot of your terminal and the last three commands you ran!





Gray check icon


Switch tabs back to your S3 console.
Refresh the Objects tab for your S3 bucket.
Do you see your new file there? 👀
Step 5: New file spotted!
Step 5: New file spotted!

Super cool 😎 A file you've created in your EC2 instance now lives in your S3 bucket too!

😮‍💨 All done
Nice work!

You've just completed today's project and learnt how to access another AWS service from your VPC.

All DONE WOOOOOOOOOOOOOOOOO!!! 🙌 High fives all round.

✅ Another AWS Service done!
What is Amazon VPC and why is it useful?

Go on, we know you have a great answer..

250 characters left


Gray check icon


🗑️ Step #7
Delete Your Resources

✋ STOP

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.



🛑 STEPS BELOW:




🪣 Delete Your S3 Buckets

Head to your S3 console.
Select your S3 bucket, and select Delete.
Enter your bucket name, and select Delete bucket.
Aha! You need to empty your bucket first. Select Empty bucket.
Type 
 in the text field.
Select Empty.
Select your S3 bucket, and select Delete.
Enter your bucket name, and select Delete bucket.
Step 7: Select Delete bucket.
Step 7: Select Delete bucket.




💻 Delete your EC2 Instance

Head back to the Instances page of your EC2 console.
Select the checkboxes next to Instance - NextWork VPC Endpoint.
Select Instance state, then select Terminate Instance.
Select Terminate.
Step 7: Select Terminate.
Step 7: Select Terminate.




☁️ Delete your VPCs

Select Your VPCs from your left hand navigation panel.
Select NextWork-vpc, then Actions, and Delete VPC.
Step 7: Select Delete VPC.
Step 7: Select Delete VPC.

Type 
 in the text box and click Delete.
Note: if you get stopped from deleting your VPC because network interfaces are still attached to your VPC - delete all the attached network interfaces first!



Other network components should be automatically deleted with your VPC, but it's always a good idea to check anyway.

Don't forget to refresh each page before checking if these resources are still in your account:

Subnets
Route tables
Internet gateways
Network ACLs
Security groups



One last thing...

Can you remmeber one last resource that we created in this project?

Do you remember one more thing to delete?!



🔑 Delete Your IAM Access Keys

Head to your IAM console.
Select Users.
Select your Security credentials tab.
Scroll down to your Access keys panel and select the Actions drop down.
Select Delete.
At the popup panel, select Deactivate, and enter your access key ID into the text field.
Select Delete.
Last but definitely not least - don't forget to delete the local access key .csv file saved on your local computer!
Step 7: Delete your access key!
Step 7: Delete your access key!

🪽 Share your work
Share your project!

Now it's time to share and let people know just what an amazing job you've done.


Share it on LinkedIn 😎‍. It's so easy - all you have to do is:


Click 'Mission Accomplished' at the bottom of this project
Select 'Mission Accomplished!'
Select 'Mission Accomplished!'

Select 'Download documentation' to download a neat PDF with all of your screenshots and work.
Select 'Download documentation'
Select 'Download documentation'

Select 'Share on LinkedIn' to open a pre-populated post, all ready to go!
Select 'Share on LinkedIn'
Select 'Share on LinkedIn'

Select the 
 at the bottom of the post - it's blocking you from uploading documentation!
Select the X at the bottom of the panel.
Select the X at the bottom of the panel.

Click on the three dots at the bottom of the panel.
Click on the three dots at the bottom of the panel.
Click on the three dots at the bottom of the panel.

Then you select this page icon, which helps you Add a document.
Add that document to LinkedIn.
Add that document to LinkedIn.

Voilà! Upload your document and give it a nice title that relates to your project.

‍Make sure to replace "@NextWork" with an actual tag 😉
Make sure to update your @NextWork tag!
Make sure to update your @NextWork tag!

Get added to NextWork's secret Hall of Fame!

Share your PDF in the NextWork community. Completing a project is literally one of the biggest achievements and milestones that everyone celebrates. Show us your amazing work. 👀

😌 And that's a wrap!
OMG

THAT'S NETWORKING PROJECT EIGHT...

DONE!!!!! 🥳

Your amazing work today!
Your amazing work today!

Today you've learnt how to:

🔑 Set up access keys for an EC2 instance: You created an access key for your EC2 instance. Now your EC2 instance can interact with your AWS services e.g. view objects in your S3 bucket!


👩‍💻 Interact with S3 through the AWS CLI: You learnt what AWS ClI does, and you ran commands to see a list of buckets and even upload an object to a bucket!



👀 A teaser for your next project...

Wooooohoo! Your EC2 instance definitely has access to your bucket - your access key worked 👏

Buttt your EC2 instance is accessing your bucket through the public internet.

This isn't the most secure way to communicate - external threats and attacks can easily intercept traffic and get access to your AWS environment or sensitive data.

What's a VPC resource that could solve this?

🥁 Introducing... VPC endpoints!

Coming up next - VPC endpoints.
Coming up next - VPC endpoints.

It's wild that all these learnings are packed in one project, and we'll see you in the next one!



To commemorate this very special occasion, we've created a one-of-a-kind trophy just for you.
To commemorate this very special occasion, we've created a one-of-a-kind trophy just for you.

🚀 p.s. Does it say "Still tasks to complete!" at the bottom of the screen? This means you still have screenshots left to upload, or questions left to answer!

Press Ctrl+F (Windows) or Command+F (Mac) on your keyboard.
Search for the text Return to later.
Jump straight to your incomplete tasks!


Message question circle icon


