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
       
## Step 8: Connecting VM to Log Analytics Workspace
* Go to Microsoft Sentinel
* Click on Log Analytics instance
* Click on Content Management -> Content Hub
* Search for **Windows Security Events**
* Install
  
* Go to Windows Security Events -> Manage
* Click on **Windows Security Events via AMA**
* Open Connector Page
* Create Data Collection Rule
* Name the rule (DCR-Windows)
* Specify Resource group and Region
* Select our Virtual Machine (CORP-NET)
* Create
  
The **AzureMonitorWindowsAgent** should reflect on the VM page

It should take some time for the logs to be loaded onto the Log Analytics Workspace.

## Step 9: Querying our Log Repository with KQL


<img width="1301" height="575" alt="az17" src="https://github.com/user-attachments/assets/f51d0807-e3b5-49e2-85db-eb3f35e4905a" />


<img width="1286" height="562" alt="az19" src="https://github.com/user-attachments/assets/9301d2fe-2147-4a77-a59d-ea4fbaaeb252" />


<img width="1267" height="529" alt="az21" src="https://github.com/user-attachments/assets/0d520b4b-28b2-456b-8c3c-be49d7957830" />


## Step 10: Uploading our Geolocation data into SIEM Sentinel
* Go to Sentinel instances and click on Watchlist
* Create a New Watchlist -> Name -> geoip -> Next -> Source
* Upload any summarized geo locations in CSV format, which contains country, latitude, longitude, and a random attacker's IP address.
* Search Key -> Network -> Create

### Step 11: Inspecting our enriched logs to see where the attacker is from
* Go to Log Analytics
* 

### Step 12: Creating the attack map






 

