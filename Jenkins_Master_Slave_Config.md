# Jenkins Master Slave Configuration Quick Reference

## Prerequisites:
1. **JDK** to be installed on master and node machines.
2. **Public** and **Private Keys** to be configured on Slave machine.

## Steps to Generate the Key pair:
1. Run the **`ssh-keygen`** command to generate the key pair 
2. The following 3 prompts are asked, hit enter by default for default config.
    * `Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa):`
    * `Enter passphrase (empty for no passphrase):`
    * `Enter the same passphrase again:`**
4. Now public and private keys are generated in the default `.ssh` folder of the user.

## Steps to be carried on Slave machine:
1. Navigate to **`.ssh`** folder, run the following command to copy the output **`cat id_rsa.pub`**
2. In the `authorized_keys` file, Paste the copied content after the already present first key.
3. Copy the private key by running the following command **`cat id_rsa`**
> *Caution: Don’t modify the already present key else you will not be able to SSH onto the slave machine*

## Steps to configure the Credentials in Jenkins
1. In Jenkins, navigate to **Manage Jenkins** --> **Credentials** --> **Add Credentials**
2. Select Kind as **“SSH UserName with private key”**
3. Enter the **ID, Description, UserName as “ubuntu”,** and **“Private key”** directly.
4. Click on **Create**

# Steps to configure the node in Jenkins:
1. In Jenkins, go to **Manage Jenkins** --> **Nodes** --> **New Node**
2. Enter a node name and select **Permanent Agent**
3. Set the **Number of Executors** (parallel jobs) for the slave
4. Create a remote working directory in the slave machine (say /home/ubuntu/vish_ws)
5. Enter the **Label** by which the Jenkins master needs to identify this slave
6. Configure Launch Method
 	* In the **Launch method"** section, select "Launch agent via SSH."
 	* Enter the following information:
   		* **Host**: IP address or hostname of the slave machine.
   		* **Credentials**: Select the dropdown with the previously configured credentials to use.
   		* **Host Key Verification Strategy**: Select **"Non verifying Verification Strategy"** for simplicity (you may want to configure proper host key verification in a production environment).
7. Click Save
8. Automatically Jenkins master will initiate a connection request with the slave.
9. You can check the status of the logs by selecting the appropriate node that was added. 

## Troubleshooting:
1. Check firewall rules for SSH and Jenkins ports.
2. Verify network connectivity between nodes.
3. Review Jenkins logs for errors.
