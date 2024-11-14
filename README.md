I have to download an OS that Wazuh can sit on. Looking at their documentation, I will choose Ubuntu. However, you could choose which ever option you are more comfortable with.

![Snag_49872d6](https://github.com/user-attachments/assets/ae7d7fc1-0c0c-4a00-8a00-ade5b88f3cfe)


Next, I had to reformat a USB using Diskpart on Windows due to the drive having been used for something else. 

Note *Make sure to run as admin first*

![Snag_49cf14a](https://github.com/user-attachments/assets/dc62b5a7-8bf3-4b4d-ba2d-d8a36c06fc9f)

Now that the drive has been reformatted back to its orginal state, I will use Balena Etcher to make the drive into a bootable USB. 

![Snag_4a6c392](https://github.com/user-attachments/assets/dbb80c89-8015-42b3-83d5-c4e9c7ea372d)


The USB has now been formated into a bootable drive


I then plug the bootable drive into my minipc and install Ubuntu on it. I went ahead and skipped gathering screenshots for this, however, I did enable RDP on the Ubuntu desktop to be able to contuine the process of documentaiton. 

![Snag_4e20251](https://github.com/user-attachments/assets/894bfaad-180d-4cbf-8832-4659d3c1fb58)

I then checked to make sure the OS is fully udpated and does not have any updates pending. 

![Snag_4e3ef3d](https://github.com/user-attachments/assets/150d911e-1328-4e38-b24c-36225a998762)

Now that everything has been checked and working as expected, its time to install the Wazuh manager on this system. 

Looking at the documentation, its time to run through the first step in which is installing Wazuh. I do the first command which is: "curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a"

![Snag_4ed9564](https://github.com/user-attachments/assets/be11fd92-c2c2-43ab-a5b7-c7085f10b778)

Wazuh is now getting configured and we just play the waiting game until it is ready

![Snag_4ef69a7](https://github.com/user-attachments/assets/6024217d-c012-414c-aac8-398a2095b39d)

The setup is now complete. Take note of the login credentials provided at the end of the install 

![Snag_4f6d60b](https://github.com/user-attachments/assets/850d05db-3637-4549-9cc4-58796ef752b3)

In order to get to the Wazuh dashboard, its going to be the local IP of the endpoint you installed it on

![Snag_4f945b3](https://github.com/user-attachments/assets/6b8406a2-c8c2-420f-832f-b1eb9859bf1f)

Once you put the IP in the URL and navigate to the dashboard, you are met with the login screen. Go ahead and put those provided credentials you got from the prevoius step and enter them in here. 

![Snag_4faac39](https://github.com/user-attachments/assets/3a6ba18a-60af-46be-ba93-bda0b93df1ac)

Once you login, you are not met with the Wazuh dashboard

![Snag_4fbaf22](https://github.com/user-attachments/assets/abe7ee27-f732-4525-bd66-7b95929edcb8)

I wanted to install an agent to talk back with the manager to start sending logs to it, so I navigated to Server Management>Endpoints Summary> then clicked on deploy new agent 

![Snag_4ff372f](https://github.com/user-attachments/assets/29a07cac-b8f1-4ce0-83de-f9f40e212202)


I am installing this on a Windows machine, so I just fill out the information required to get the powershell command at the end to install it

![Snag_502579a](https://github.com/user-attachments/assets/be68d367-3a11-4e93-81ff-4016edbd2d2e)

I now head back over to my Windows desktop and launch powershell as admin and load up the script

![Snag_5041586](https://github.com/user-attachments/assets/3c1a8a92-3015-4beb-8926-abd7f084e982)


I then start the service as well 

![Snag_5059abf](https://github.com/user-attachments/assets/da3218d6-bf05-4c8d-8b7b-f741baaa5e16)


Now that the serivce has started, I head back over to the Wazuh manager to see if the agent is checking in. 

Looks like the agent is successfully checking in with the Wazuh manager now 

![Snag_506f9f1](https://github.com/user-attachments/assets/3325e10e-ad08-4054-bdc7-cad904c0be6c)

I now let the agent sit on the desktop to start collecting telemetry about the desktop and it looks like its already logging Windows event logs by showing my login activity 

![Snag_50bb59c](https://github.com/user-attachments/assets/c9c09112-9c6e-4237-8d1e-5a5b34a302bb)



Conclusion: I have successfully installed Wazuh manager on a Ubuntu OS and downloaded an agent onto a Windows desktop to check in and start sending logs to the manager. The agent needs to sit on the device and start collecting data which takes time, but overall the process was fun and gave great insight on how to setup a SIEM tool. 
