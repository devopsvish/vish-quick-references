# Jenkins Master Slave Configuration Quick Reference

## Prerequisites:
	1. JDK to be installed on master and node machines.
	2. Public and Private Key to be configured on Slave machine.

## Steps to Generate the Key pair:
	1. Type the below command to generate the key pair 
         a. `ssh-keygen`
	2. Below 3 prompts are asked, hit enter by default for default config.
         a. `Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa):`
         b. `Enter passphrase (empty for no passphrase):`
         c. `Enter the same passphrase again:`
	3. Now public and private keys are generated in the default .ssh folder of the user.

## Steps to be carried on Slave machine:
	1. Navigate to .ssh folder, run the below command and copy the output.
         a. `cat id_rsa.pub`
	2. Paste the copied content after the first key. 
         a. Note: Don’t modify the already present key else you will not be able to SSH onto the slave machine
	3. Copy the private key by running the below command
         a. `cat id_rsa`

## Steps to configure the Credentials in Jenkins
	1. In Jenkins, navigate to Manage Jenkins --> credentials --> Add Credentials 
	2. Select Kind as “SSH UserName with private key”
	3. Enter the ID, Description, UserName as “ubuntu”, and “Private key” directly. Click on Create

# Steps to configure the node in Jenkins:
	1. In Jenkins, go to Manage Jenkins à Nodes à New Node.
	2. Enter a node name and select "Permanent Agent"
	3. Set the Number of Executors (parallel jobs) for the slave
	4. Create a remote working directory in the slave machine (say /home/ubuntu/vish_ws)
	5. Enter the Label by which the Jenkins master needs to identify this slave.
	6. Configure Launch Method:
         a. In the "Launch method" section, select "Launch agent via SSH."
         b. Enter the following information:
             i. Host: IP address or hostname of the slave machine.
             ii. Credentials: Add a new SSH username with private key credential using the private key generated earlier.
             iii. Host Key Verification Strategy: Select "Non verifying Verification Strategy" for simplicity (you may want to configure proper host key verification in a production environment).
	7. Click Save. 
	8. Automatically master will try to establish the connection with the slave. You can check the logs by selecting the appropriate node that was added. 

## Troubleshooting:
	1. Check firewall rules for SSH and Jenkins ports.
	2. Verify network connectivity between nodes.
	3. Review Jenkins logs for errors.
