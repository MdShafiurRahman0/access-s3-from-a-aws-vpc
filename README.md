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


5. For the Amazon Machine Image, select Amazon Linux 2023 AMI.

6. For the Instance type, select t2.micro.

7. For the Key pair (login) panel, select  Proceed without a key pair (not recommended).

8. At the Network settings panel, select Edit at the right hand corner.

9. Under VPC, select NextWork-vpc.

9. Under Subnet, select your VPC's public subnet.



![image](https://github.com/user-attachments/assets/eb513560-8671-4c7b-b84e-b1337ad555e1)


![image](https://github.com/user-attachments/assets/21fd5f62-c244-4ab7-9902-6901616bcc23)




# Step 3: Connect to Your EC2 Instance


![image](https://github.com/user-attachments/assets/e1eeda60-2bbc-4494-a2cb-03217d208519)


![image](https://github.com/user-attachments/assets/71ffb230-60f0-4159-98f9-66d17d9e6077)


1. Run aws configure
2. The terminal is now asking us for an Access Key ID!

![image](https://github.com/user-attachments/assets/102630f7-002d-4e57-8288-10d72b2ddc32)



# Step 4 : Create Access Keys


![image](https://github.com/user-attachments/assets/10154504-25a2-419a-9d92-6f0ab4b68518)


1.Search for in the search bar Access Keys

2.aha! So it's the IAM console that helps us set this up. Select IAM.


![image](https://github.com/user-attachments/assets/6b68bf54-a231-478d-81ae-8929fef204e8)


## Search for Access Keys again in the IAM console's left hand navigation panel.


![image](https://github.com/user-attachments/assets/52bf64d7-3b6c-442d-be51-c673f98b4fe2)


![image](https://github.com/user-attachments/assets/7ad34e13-6811-434f-a49d-a68d11901afd)

![image](https://github.com/user-attachments/assets/50346438-c72b-41df-b494-c1b9143474b2)


![image](https://github.com/user-attachments/assets/d26ddac0-ca3f-42da-912e-c15912605b67)


## Select Create access key.



![image](https://github.com/user-attachments/assets/839606fa-4b65-4d13-9941-24ba655c13d0)


# Step 5 : Create an S3 bucket with 2 files

![image](https://github.com/user-attachments/assets/7d464872-8dc5-43b2-a926-6698ee6d626c)

![image](https://github.com/user-attachments/assets/a8da84b9-8fd1-4ea8-8242-5a526ddcc00e)

![image](https://github.com/user-attachments/assets/45d61a91-6eb2-4a98-bbec-283b3566eb78)

![image](https://github.com/user-attachments/assets/2cd353f3-6d27-4109-a438-beb93945e4b0)

![image](https://github.com/user-attachments/assets/79ca1413-45dc-4c01-a66f-41c9a28455e1)



## Select two files in your local computer to upload.

![image](https://github.com/user-attachments/assets/3db7a71b-bdfe-4dc8-a147-ba112efa0c14)


# Step 6 : Connect to your S3 bucket


![image](https://github.com/user-attachments/assets/d9834eb3-7380-42d8-aa7d-8d921343b4af)

1. Open the AccessKeys.csv file you've downloaded.
 
2. Copy the Access key ID.


![image](https://github.com/user-attachments/assets/aca680a6-6dd1-4635-a124-ee2d931603df)


3. Let's do the same for the AWS Secret Access Key!

4. Copy the key from your .csv file, and paste it in the terminal. Press Enter.

5. Next, for your Default region name, open your Region dropdown on the top right hand corner of your AWS console.

6. Copy your Region's code name. For example, us-west-2.


![image](https://github.com/user-attachments/assets/1702963c-0deb-4b96-948a-59a108512360)

![image](https://github.com/user-attachments/assets/d5cf5bab-b0f6-4b5e-96b8-5b7289a2403d)



## Type Command : aws s3 ls

![image](https://github.com/user-attachments/assets/2a8e9688-ccd2-4984-8d43-b67b0731bb98)


![image](https://github.com/user-attachments/assets/510e3a32-fcda-439a-88f2-8aa3c8b6d0f8)











