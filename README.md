

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/b233cad0-4420-4f46-839a-c5e63ffc8100" />


# Deployment of Honeypot in Azure's cloud utilizing T-pot


# Steps Taken to implement this project. 

## 1.  Create resource group. Once the Azure account has been created and the subscription is set up, I started by creating a resource group. This is basically a folder/container where all the resources for this lab reside, for example, the virtual network, the VM, and other components. 

- From the dashboard, click on resource groups, give it a name, and click on review and create
  
  <img width="1093" height="170" alt="image" src="https://github.com/user-attachments/assets/9e3037a0-7431-425e-8bff-97fb8cd3c407" />
   

  <img width="753" height="760" alt="image" src="https://github.com/user-attachments/assets/68c3becd-74d0-44b1-9a3a-453e410f620f" />

## Step 2 Create the virtual network. Here I created the virtual network.

- The virtual network is basically, our network structure to which the VM running the honeypot will use to connect to the internet.
  
- From the Azure dashboard or in the search bar find and select Virtual networks
- Then name the virtual network. The IP address space can be left as default.
- Then click review and create > Create.
  
  <img width="103" height="122" alt="image" src="https://github.com/user-attachments/assets/e186a1aa-59ab-4757-94db-bc1eda3da6fb" />
  

  <img width="864" height="659" alt="image" src="https://github.com/user-attachments/assets/f87210ac-b73d-4ebd-bab5-310ce8b45e36" />
  

  <img width="812" height="785" alt="image" src="https://github.com/user-attachments/assets/13977386-8f49-4418-a7a2-fa3bf59e59a1" />


## Step 3: Create the virtual machine. In this step I created the VM that will run the Honey pot. 

- This VM will be running Ubuntu Pro 24.04 LTS
- Similar to previous steps, go to the Azure dashboard or find  and click on virtual machines from the search bar at the top
- In this step, I named the VM, selected the region, selectected the image (Ubuntu in this case), and created a user and password. For simplicity and the sake of this lab, I created a user and password instead of using a public/private key, whicch is always recommended.


 <img width="871" height="763" alt="image" src="https://github.com/user-attachments/assets/86352bb9-7cff-4680-8278-d9f1e2087550" />

 <img width="506" height="707" alt="image" src="https://github.com/user-attachments/assets/b8469ad1-e470-41c5-aa65-da4d022c9677" />

Note: During this step, I left the defaults, for management, monitoring, advanced and tags

## Step 4: SSH into the created VM

- During this step, I SSHd into the VM and updated its repositories using the following commands: (The public IP address can be obtained from the overview page of the VM after creation)

  - To login into the VM:
    `ssssh username@Public IP`
- If login is successful, we should be presented with somethhing similar to the image below:

  <img width="765" height="567" alt="image" src="https://github.com/user-attachments/assets/ee5c1d1d-da87-4a30-a6f6-efc4062ac416" />

  - Update repositories ( This commandd line will update and upgrade the packages )
    `sudo apt update && sudo apt upgrade -y`

  <img width="964" height="571" alt="image" src="https://github.com/user-attachments/assets/ec432e34-1e2d-4687-b727-e8e0d9cce5d7" />

# Step 5: Add sample user account
  `sudo adduser username`

  - Once the user is created, add the user to the sudo group.

    `sudo usermod aG sudo username`
  - Then switch to the created user
    `su username`

   <img width="717" height="423" alt="image" src="https://github.com/user-attachments/assets/b01431bf-16ad-41d7-8d73-218624ab2e6a" />

   <img width="668" height="168" alt="image" src="https://github.com/user-attachments/assets/fc93cbfd-d067-42fc-8ea3-512d19429b1c" />

 - Then, change to the diretory of the created user
   we can confirm we are logged in as the created user using: `whoami`
   to change to this user's directory: `cd ../user`

   <img width="477" height="233" alt="image" src="https://github.com/user-attachments/assets/fe8847fa-bb93-4a53-8e64-13b43e6d06e5" />


## 5 Step 6: Clone Tpot's repository. 

  To clone the repository : `git clone https://github.com/telekom-security/tpotce.git` 

  - This will download a folder into the user's home directory. Once downloaded, go into that directory: `cd \tpotce`
  - From here the files within the directory can be listed using `ls -l`. There should be a file named install.sh
  - Then run `.\install.sh` to run the script and install the Tpot application

   <img width="718" height="131" alt="image" src="https://github.com/user-attachments/assets/88a2853b-bd99-4a8d-88ef-563e3b90f8d9" />

   <img width="659" height="166" alt="image" src="https://github.com/user-attachments/assets/273c7467-3c3d-47bf-8d38-e70cc08c4211" />

   <img width="1027" height="981" alt="image" src="https://github.com/user-attachments/assets/0a40935b-777a-44ee-8453-90e0307f4617" />

 - The installation process should take about 2 to 4 minutes. During this time all Tpot's dependecies should be installed.

   <img width="1876" height="961" alt="image" src="https://github.com/user-attachments/assets/bfcf1516-4457-423c-ae2b-d237f5f95a05" />

   Note that the SSH port will be changed during the installation process. This means that to log back into the Honey pot, that new port would b used instead

   <img width="1301" height="57" alt="image" src="https://github.com/user-attachments/assets/99ec4ca0-48f2-4095-9aab-d226edcbdb00" />

-  A prompt asking for the type installation will be presented, in this case, select option h, for hive installation. Then enter a username and password.

   <img width="1066" height="557" alt="image" src="https://github.com/user-attachments/assets/d22ece2c-86b5-4260-861a-c1e2bca4b9f3" />

   
   ![Tpot](https://github.com/user-attachments/assets/2c247470-2962-4395-820e-bd54752d6c19)

  - If the installation succeeded, something like this would be presented on screen:

   <img width="1176" height="268" alt="image" src="https://github.com/user-attachments/assets/0c4a4edc-5d86-4c21-b387-015504f0cec5" />

  Once the reboot completes, we can ssh back using the new port that was set during the installation. 

  - Depending on the cloud provider, you may need to edit the firewall's inbound rules. In this case, since the port number changed, This can be done from the NSG (Network Security Group). This is basically a type of firewall offered in Azure.
  -  This can be done from within NSG: Find NSG in the search bar > click on the NSG that should've been created automatically when setting up the VM and Virtual network. 

   <img width="499" height="166" alt="image" src="https://github.com/user-attachments/assets/47c8946b-49f9-417c-a509-79444496a9d5" />
   
   <img width="1506" height="57" alt="image" src="https://github.com/user-attachments/assets/ce6e353b-97a4-4ea3-ae1b-b8d9086dfc2c" />

   From here : Settings > Inbound rules > Add
   <img width="1313" height="350" alt="image" src="https://github.com/user-attachments/assets/5436b17a-b0f9-4063-a357-74afcc895f67" />


  ## Step 7: Log into the Tpot GUI (Tpot listens for web requests on port 64297)

  - From the local computer log into Tpot's GUI by navigating to https://{public_ip}:64297
  - We may be presented with the following message. In this case, we can click on proceed, and log in using the credentials created during the installation process of Tpot.

   <img width="727" height="457" alt="image" src="https://github.com/user-attachments/assets/7bc11131-ee4f-4cd4-9b7f-493b2ede9cfa" />


-  After successfully loging in, we are presented with a screen as shown below. Some interesting options are the Attack map, Kibana, and

  ![tpot-home](https://github.com/user-attachments/assets/0e2a51a1-e653-415c-9a49-88227225dded)

  1. The Attack map will display the geolocation from where attacks originate, a table is populated with different details such as IP address, country,etc. This dashboard will also include the type of service being attacked. The longer this VM is left ON, the more attacks and locations that will start to show up.

     ![map1](https://github.com/user-attachments/assets/9ba4cb84-dafc-4645-aab2-1fb6c7ffb605)

     ![map2](https://github.com/user-attachments/assets/3dcfd87a-3676-4b97-8c41-c6c633ba1073)

     ![map3](https://github.com/user-attachments/assets/b0328165-ea67-422a-9ada-ac0cf1ed9e85)


 2. Kibana, will provide us with a dashboard, that will include a breakdown of the attacks, locations, IP, OS, service, CVE, and more. We can interact with this dashboard, by clicking on the panels, filtering, and using queries written in KQL. 

    <img width="1890" height="708" alt="image" src="https://github.com/user-attachments/assets/3191cbc4-25d5-4218-9874-f8e090f8099b" />

    <img width="1894" height="800" alt="image" src="https://github.com/user-attachments/assets/5ab7b2e1-482a-4cb6-b254-377c74b377bb" />

    <img width="1884" height="456" alt="image" src="https://github.com/user-attachments/assets/66826c12-54f5-4e20-9b5d-55a94a2d440f" />







  




  



  






    


  

  








  
