# Cloud-SOC-Lab-using-Azure-and-Analysis-of-Live-Cyber-Attacks
Setting up a SOC lab using Azure, creating a virtual machine (VM) as a Honeypot, configuring the log forwarding into the central repository, which is Log Analytics Workspace, ingesting logs to Sentinel SIEM by connecting the Log Analytics for querying, creating an attack map, and analyzing the live cyber attacks.

## Step 1: Creating Resource Group
* Log in to the  Azure portal
* Go to Resources and create
* Select Azure Subscriptions
* Name the Resource group (RG-SOC-Lab)
* Select Region and Create
## Step 2: Create a Virtual Network
* Click on Create Virtual network
* Select the same resource group and region
* Name the Vnet (Vnet-soc-lab)
* Review+Create
## Step 3: Create Virtual Machine(VM) 
* This is going to be our Honeypot
* Click on Create Virtual Machine
* Select the resource group
* Name the VM (CORP-NET)
* For image -> windows 10 pro
* select size -> Standard ds2 version
* Create a Username and password
* Select Disk -> Premium SSD
* Select Vnet for networking
* Enable delete public IP when VM is deleted
* Disable Boot Diagnostics
* Create
## Step 4: Opening the Firewall of VM
* Go to resource group and select the firewall *nsg*
* Delete the RDP rule in the Inbound rule
* Settings -> Inbound Security rules -> Add
* Set destination port to any
* Name the rule (Danger-AllowAnyCustomInbound)
## Step 5: Power up the VM
* Copy the Public IP of VM
* Paste it on the Remote Desktop Connection on your host machine
* Log in using the username and password created

     ### Turn off the Windows Firewall on VM
        * Go to Windows Firewall
        * Click on Windows Defender Firewall Properties
        * Turn off all the profiles
       
  Ping the VM from the local computer to check the connectivity **ping <Public IP of VM>**
  
## Step 6: Viewing Raw Logs On Virtual Machine
* Try to log in with different accounts and create multiple failed logins
* Go to VM and open Event Viewer to view local logs
* Windows Logs-> Security Events
* You can notice a bunch of security events of failed login attempts with event code **4625**

 We can now forward these logs into Azure Sentinel by creating a **Log Analytics Workspace** and connecting it to the SEIM Sentinel
## Step 7: Creating Log Analytics Workspace (our Log Repository)
* Click on Create Log Analytics Workspace
* Specify the Resource Group
* Name the Log Analytics and Region
* Review and Create
  
   ### Adding Microsoft Sentinel to Log Analytics Workspace
     * Go to Sentinel
     * Click on Add Sentinel to Workspace
     * Select the created workspace and create
  
 
  

 

