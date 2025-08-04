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
* Select Disk
* Select Vnet for networking
* Enable delete public IP when VM is deleted
* Disable Boot Diagnostics
* Create
  
* 
* 

