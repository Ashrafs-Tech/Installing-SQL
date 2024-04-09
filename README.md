# Firewalls and installing SQL Server

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/787c86f5-3dab-4259-a411-9fb4a98ff523)


## Intro

In this section of the project I will be doing three things:

- Disable the internal Windows Firewall
- Install MS SQL Server
- Install and configure SQL Server Mangnement Studio

## Disable the Firewall

In the previous step, I opened up the Network Security Groups to allow all inbound traffic. Network Security Groups are like a firewall for Azure. 

Now I will disable the internal Windows Firewall with the Remote Desktop Connetion application built into my main Windows computer. 

First I will need to copy the public IP address of my Windows virtual machine. Then I logged into it. 

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/f66cd6e6-b9ba-42ca-81a5-ee79e572851f)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/6ccabeaa-b3ed-4c04-9623-238d59e58fa4)

The reason why I want to disable the Windows Firewall is because I want to make it easier for the virtual machine to be discovered by malicious actors. 

To do this:
- In the start menu of the Windows virtual machine, I will type in "wf.msc".
- Click Windows Defender Firewall Properties
- Turn of Domain, Private, and Public profile and then click "Apply"


![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/822f04cc-07e8-4025-83e6-784e0afdc2e2)
![VL 16](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/d3f56c14-2b27-45b7-ab89-81db11a6e918)
![VL 17](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/3fc21975-4b7f-44f7-b236-1141ec7c3016)


## SQL Server Evaluation installation

Now that the firewall has been disabled, I will focus on installing the SQL Server Evaluation into my Windows virtual machine. The reason I am downloading this is because it will serve as another attack vector for malicious actors. 

To do this:
- I will go on Microsoft Edge on the virtual machine.
- Search for "SQL Server Evaluation"
- Download the EXE to install it

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/a514e6ba-88cc-4889-abf5-96bd7563a5d0)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/fe338a26-e3fc-4ac3-b2c4-8d1f19be1fc3)

- During the downloading process, I will use the defualt username they give me "sa" and I will use the password I used for my virutal machines.
- I will click the button "Add Current User" which will add the Windows virtual machine.
- Then click "next" and "Install"

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/7b1ab090-0a6f-443c-ad38-972682f1adfe)


## SQL Server Management Studio installation and configuration

The reason why I will download the Management Studio is because it will allow us to login to the SQL Server and be able to generate logs of failure to authenticate. 

To do this:
- Go Microsoft Edge in our virtual machine
- Search "Download SMSS"
- Scroll down and click the download link


![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/4e39db4a-010f-48e1-b215-b98d5c25b659)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/24df87a9-5f6f-47fc-bef2-4a6add6cf741)


Now that it's downloaded, I will need to enable logging for the SQL Server. But first I will show how to view the logs

In order to do this: 

- I go to Event Viewer
- Click on Windows Log
- Click on Security

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/dd8c6bd0-233f-49f3-ad64-e9ab9b6748a1)

This will show the logs. Whenever someone has a failed or successful login, it will be recorded in the Event Viewer.  

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/9a112076-6499-4a73-863c-22e4274052d3)

Now in order to enable the logs:

- I will go to Registry Editor
- Click on HKEY_LOCAL_MACHINE
- Click system
- Click CurrentControlSet
- Click Services
- Click Event Log
- Click Security
- Right click Permissions

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/b6480d50-ee66-4aec-9dac-dc400d0d2cb5)

- Then click "Add"
- Type in NETWORK SERVICE and click OK

  ![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/5938942c-33c6-44cc-a1cc-5c892d4fcc45)
  ![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/21e0dac7-c24a-4a3c-b158-197456b3dec3)

- Then open command line and input the following text and then click enter
  
  ![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/e59b386d-99c2-46aa-a09c-642908530c07)

- Open up SQL Server Managment Studio in the menu bar
- Login with the "sa" username and the password
- Right click on the server to click Properties
- Click on Security
- Under "Login auditing", select "Both failed and successful logins" so to that they can be logged to the event log
- Finally, go back to the server, right click and look for the Restart option to finish the configuration.

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/071b2252-3f12-40a9-8910-02ad54d46d00)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/eca562c4-9d1b-4951-8a85-956ce8d89f5a)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/18d785c1-45f0-462c-96c0-f2c8d24aba01)
![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/626bb39d-fe41-4ae8-9195-cff343d84722)

*Remember that we have not sent any logs to a central repository yet.  All these logs only exist in the virtual machine.  The transfer will happen in the next steps. 


## Step 2 is done. 
- Firewalls disabled
- SQL Server installed
- SQL Server properly configured.

![image](https://github.com/Ashrafs-Tech/Installing-SQL/assets/166546026/19ea8805-d930-4412-8ca4-e08662910692)











