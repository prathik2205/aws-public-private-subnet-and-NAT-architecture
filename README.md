# aws-public-private-subnet-and-NAT-architecture
This Project demonstrates how to create a VPC that you can use for servers in a production environment. You deploy the servers in two Availability Zones, by using an Auto Scaling group and an Application Load Balancer. For security, you deploy the servers in private subnets. The servers receive requests through the load balancer
## Overview :
This project's overview is depicted in the diagram below. The setup revolves around a Virtual Private Cloud (VPC) featuring both public and private subnets, thoughtfully distributed across two Availability Zones to ensure reliability.

Within each public subnet, there's a NAT gateway to facilitate outbound internet connectivity and a load balancer node for effective traffic distribution.

On the other hand, the project's servers reside in the private subnets. Their deployment and termination are automated through an Auto Scaling group, allowing them to dynamically adapt to workload changes. These servers play a pivotal role in receiving traffic from the load balancer and can access the internet through the NAT gateway when necessary


<img width="611" height="481" alt="img 1" src="https://github.com/user-attachments/assets/f4e1d65a-d36b-400e-9f68-07c74a3763f1" />

## Steps :
### Step 1 :
#### Create the VPC :
1. Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.
2. On the dashboard, click on "Create VPC."
3. Under "Resources to create," select "VPC and more."
4. Configure the VPC:<br>
   a. Provide a name for the VPC in the "Name tag auto-generation" field.<br>
   b. For the IPv4 CIDR block, leave it as default suggestion.<br>
5. Configure the subnets:<br>
   a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.<br>
   b. Specify the "Number of public subnets" as 2.<br>
   c. Specify the "Number of private subnets" as 2.<br>
   d. For NAT gateways, choose "1 per AZ" to enhance resiliency.<br>
   g. For VPC endpoints, you can choose "None" .<br>
   h. Regarding DNS options, clear the checkbox for "Enable DNS hostnames."<br>

   Once you've configured all the settings, click "Create VPC."

   <img width="1913" height="870" alt="img2" src="https://github.com/user-attachments/assets/c00cf1ad-4d03-41c8-965b-f11f8cc8f2ac" /><br><br>

   <img width="1918" height="871" alt="img3" src="https://github.com/user-attachments/assets/00ebede9-0459-4f48-a7c3-a2069c1a52f0" /><br>

   <img width="1918" height="868" alt="img4" src="https://github.com/user-attachments/assets/a87ad728-4998-415f-b2c6-0781cd544f1e" /><br>

   <img width="1918" height="871" alt="img5" src="https://github.com/user-attachments/assets/fa764864-f742-4b98-a162-a12da97b4d7c" /><br>

 6. Now you can see you are successfully Created VPC .


### Step 2:
#### Creating the Auto Scaling Group :

<img width="1917" height="877" alt="img1" src="https://github.com/user-attachments/assets/38504bf8-4f86-4067-9941-66f69dacc122" /><br>

<img width="1917" height="875" alt="img2" src="https://github.com/user-attachments/assets/dff9da45-4652-449d-b8d6-9b2529c72458" /><br>

<img width="1918" height="875" alt="img3" src="https://github.com/user-attachments/assets/749e4829-b6d6-4974-9318-a164221bba84" /><br>

<img width="1916" height="877" alt="img4" src="https://github.com/user-attachments/assets/901b8b68-c53d-4bea-93cd-aaba1988060a" /><br>

<img width="1918" height="871" alt="img5" src="https://github.com/user-attachments/assets/7ebb47da-5fc6-4486-b1ea-51a8c84f5c3c" /><br>

1. Now you have to choose the Key-pair you created.<br>

<img width="1918" height="875" alt="img6" src="https://github.com/user-attachments/assets/b25220fe-6a74-488a-ad27-52aacc6ea720" /><br>

<img width="1918" height="872" alt="img7" src="https://github.com/user-attachments/assets/11637147-aee4-4f39-b1c1-be747be4f248" /><br>

<img width="1918" height="871" alt="img8" src="https://github.com/user-attachments/assets/2f7b23f9-f28b-4422-9623-9d3672fa4d28" /><br>

<img width="1917" height="882" alt="img9" src="https://github.com/user-attachments/assets/3677d873-9bae-4a8f-b5e2-b2d18e25ba76" /><br>

<img width="1918" height="876" alt="img10" src="https://github.com/user-attachments/assets/6d37dd44-8ad7-40a0-91de-4bf5f86441dd" /><br>
2. Scroll Down and then Click "Next".

<img width="1918" height="876" alt="img11" src="https://github.com/user-attachments/assets/1d99909f-2562-4e3a-a878-8c39de7f828a" /><br>
3. Scroll Down and then Click "Next".

<img width="1918" height="872" alt="img12" src="https://github.com/user-attachments/assets/0dd7a0fd-2e91-4870-94da-2a82cfd8ecef" /><br>
4. Scroll Down and then Click "Next".

<img width="1918" height="877" alt="img13" src="https://github.com/user-attachments/assets/3ef9b81b-f394-4194-97df-9f8ef3aeed43" /><br>
5. Scroll Down and Click "Skip to Review".

<img width="1917" height="870" alt="img14" src="https://github.com/user-attachments/assets/babb6045-4302-4c53-92de-828dd677c284" /><br>

6. Now your are Successfully Created Auto Scaling Group.<br>
7. Open the AWS Management Console.<br>
8. Navigate to the EC2 console by clicking on "Services" in the top-left corner, then selecting "EC2" under the "Compute" section.<br>
9. In the EC2 dashboard, you'll find the "Instances" link on the left-hand navigation pane. Click on "Instances."<br>
10. Here, you should see the list of EC2 instances associated with your account. Look for the instances created by your Auto Scaling Group.<br>
Since you mentioned that the Auto Scaling Group launched instances in different AZs, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple AZs.

### Step 3 :
#### Creating the Bastion Host :

1. Launch Instance as Specified below.

<img width="1918" height="873" alt="img1" src="https://github.com/user-attachments/assets/ca5a9354-3782-46ae-8da7-ef1ba0a50670" /><br>

<img width="1918" height="866" alt="img2" src="https://github.com/user-attachments/assets/a78b53a7-519e-4075-b6dd-3b843e50a4eb" /><br>

<img width="1918" height="873" alt="img3" src="https://github.com/user-attachments/assets/6c0fc48e-216c-47af-845f-ce271ccd785a" /><br>

<img width="1918" height="870" alt="img4" src="https://github.com/user-attachments/assets/f3907aa0-a606-4977-8801-97a9ce24b03e" /><br>

<img width="1918" height="872" alt="img5" src="https://github.com/user-attachments/assets/fb7961ca-4cb3-4da5-9f1c-ef8e44014602" /><br>

### Step 4: 
#### SSH into Private Instance

1. SSH into the Bastion Host Instance:
   To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we'll be able to SSH into the private instance.
2. Ensure the PEM File is Present on the Bastion Host:
   Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won't be able to SSH into the private instance from the Bastion host.
3. Open a Terminal:
   Open a terminal window on your local machine.
4. Execute the Following Commands:<br>

   a. If your PEM file is named something like `<aws demo.pem>`, you must remove spaces in the filename. Please rename the file to something like `<aws_demo.pem>`.<br>
   
   b. Copy the PEM file to the Bastion host using the `scp` command. Replace `<pem file location>` with the local and remote file paths, and `<bastion host public IP>` with the Bastion host's public IP address. <br>
   
   Example:
   ```
       scp -i /c/Users/welcome/Downloads/aws_demo.pem /c/Users/welcome/Downloads/aws_demo.pem ubuntu@18.60.214.205:/home/ubuntu
      ```
   c. The above command will copy the PEM file from your computer to the Bastion host. Once the file is successfully copied, move on to the next step.<br>
   
   d. SSH into the Bastion host using the following command:<br>
   
   ```
      ssh -i aws_demo.pem ubuntu@18.60.214.205
      ```
   
 <img width="1906" height="1020" alt="img1" src="https://github.com/user-attachments/assets/9a5f2fc3-16c9-4de7-994e-c0a9d7ee7d6e" /><br>

 e. After SSHing into the Bastion host, use the `ls` command to check if the `aws_demo.pem` file is present. If it's not there, double-check your previous commands.<br>
 
 
    
      



















