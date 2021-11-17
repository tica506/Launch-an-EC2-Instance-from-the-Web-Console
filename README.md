
1.  Click Open AWS console to access the lab environment, then use the provided credentials to log in. Note: Ensure you are in the US West (Oregon) region in the top-right corner of your screen.
	
2. Use the search bar at the top to navigate to the EC2 service. 
	
3. Click the Launch instance button and then click Launch instance.
	
4. At the top of the list of AMIs on the Choose an Amazon Machine Image start page, click the Select button for the option labeled Amazon Linux 2 AMI (HVM), SSD Volume Type. Keep the radio button for 64-bit (x86) selected. Note: This Quick Start page allows you to choose from a variety of different Amazon approved Quick Start images. Options include: Amazon Linux, Red Hat, Suse, Ubuntu, and Windows. Amazon curates this selection of Quick Start options and vendors must agree to continually update the images that appear here, to ensure they are kept up-to-date with security patches. Note: If you wanted to launch an EC2 option from an AMI (Amazon Machine Image) that does not appear in the limited Quick Start list, you could select from the other tabs on the left hand side. These options include My AMI's (for images your organization has built themselves), AWS Marketplace (which includes AMI's from many different vendors, often using a pay per minute model), and Community AMI's, where you can find images for additional operating systems, such as CentOS and Debian. 
	
5. On the Choose an Instance Type page, keep the t2.micro instance type selected, then click the Next: Configure Instance Details button at the bottom right. This instance type creates a virtual machine with 1 vCPU (virtual CPU) and 1 GiB of memory. 
Note: Notice that the t2.micro instance type has a green label for "Free tier eligible." AWS offers a free tier that allows you to launch and run a t2.micro instance for 1 year without incurring any charges. Be aware that, if this were your own AWS account, other AWS services may cause your account to incur charges – but it is possible to run some things in AWS for a year without paying anything, thanks to the generous Free tier.
	
6. On the Configure Instance Details page, review the available options, but keep the defaults selected. Scroll down to the Advanced Details section and expand it if it is collapsed.
	
7. In the User data section, keep As text selected, and then paste the following lines into the text box:
#!/bin/bash -xe
yum install -y ruby
cd /opt
curl -O https://aws-codedeploy-us-west-2.s3.amazonaws.com/latest/install
chmod +x ./install
./install auto
Then click the Next: Add Storage button at the bottom right.
Note: The above script will download and install the AWS CodeDeploy agent immediately after the EC2 instance is launched. The usage of EC2 User data scripts is the most common way to initialize or bootstrap EC2 virtual machines.

8. On the Add Storage page, review the EBS (Elastic Block Store) Volume attributes, keep the default 8 GiB size, and then click the Next: Add Tags button at the bottom right.

9. On the Add Tags page, click the Add Tag button, enter a Key of env and set its Value to test. 

10. Add another tag with the Key Name and the Value webserver1. 
Note: The Name tag (case sensitive) is a special tag that AWS uses to display the user-defined instance name on the Instances web console page.
Notice that these tags will be applied to both the EC2 instance and the EBS volume. 

11. Click the Next: Configure Security Group button.

12. On the Configure Security Group page, keep the Create a new security group radio button selected, keep the default Security group name of launch-wizard-1, and keep the auto generated Description. 
Notice that the launch wizard has populated a single Security Group Rule with Type: SSH, Protocol: TCP, Port Range: 22, and Source: 0.0.0.0/0 (this means any IP address). This rule opens up access for the entire internet to SSH into the EC2 instance on port 22.

13. Click the Review and Launch button.
Note: For any AWS account and EC2 instance of real importance, you should never use a Security group named after the launch-wizard, and you should not allow SSH access from the entire internet. Instead, you should give your Security Group a name that is descriptive of its purpose or function, and you should use a VPN or a Bastion host for SSH access into your EC2 instances.

14. On the Review page, you can review all of the options that you have selected throughout the Launch wizard process. Click the Launch button at the bottom right.

15. You will now see a Select an existing key pair or create a new key pair modal. Click on the Choose an existing key pair dropdown and select Proceed without a key pair, then add a checkmark to the acknowledgement box that informs you that you will not be able to connect to the instance. 

16. Click the Launch Instances button.
Note: Typically when launching an EC2 instance you would create and select an existing key pair that you've already added to your AWS account. This key pair allows you to SSH into the EC2 instance using the default user.
After a brief Initiating Instance Launches page, you'll be taken to a Launch Status page, and you should see a green box at the top of the page that says Your instances are now launching. You should also see a unique instance identifier, which looks like i-XXXXXXXXXX.
