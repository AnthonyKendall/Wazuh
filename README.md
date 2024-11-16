# Wazuh

## Objective

Wazuh is an open-source security monitoring platform that provides real-time threat detection, log analysis, and vulnerability monitoring. It helps organizations detect security incidents, ensure compliance with regulations, and respond to potential threats effectively. Setting up and practicing with Wazuh is valuable because it allows hands-on experience with a powerful tool that integrates seamlessly with other security solutions like the Elastic Stack, enabling a comprehensive view of security data. This experience is crucial for improving skills in monitoring, incident response, and maintaining a strong security posture across diverse environments.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.



## Steps Taken

I have to download an OS that Wazuh can sit on. Looking at their documentation, I will choose Ubuntu. However, you could choose which ever option you are more comfortable with.

![Snag_49872d6](https://github.com/user-attachments/assets/ae7d7fc1-0c0c-4a00-8a00-ade5b88f3cfe)


Next, I had to reformat a USB using Disk part on Windows due to the drive having been used for something else. 

Note *Make sure to run as admin first*

![Snag_49cf14a](https://github.com/user-attachments/assets/dc62b5a7-8bf3-4b4d-ba2d-d8a36c06fc9f)

Now that the drive has been reformatted back to its original state, I will use Balena Etcher to make the drive into a bootable USB. 

![Snag_4a6c392](https://github.com/user-attachments/assets/dbb80c89-8015-42b3-83d5-c4e9c7ea372d)


The USB has now been formatted into a bootable drive


I then plug the bootable drive into my minipc and install Ubuntu on it. I went ahead and skipped gathering screenshots for this, however, I did enable RDP on the Ubuntu desktop to be able to continue the process of documentation. 

![Snag_4e20251](https://github.com/user-attachments/assets/894bfaad-180d-4cbf-8832-4659d3c1fb58)

I then checked to make sure the OS is fully updated and does not have any updates pending. 

![Snag_4e3ef3d](https://github.com/user-attachments/assets/150d911e-1328-4e38-b24c-36225a998762)

Now that everything has been checked and working as expected, its time to install the Wazuh manager on this system. 

Looking at the documentation, its time to run through the first step in which is installing Wazuh. I do the first command which is: "curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a"

![Snag_4ed9564](https://github.com/user-attachments/assets/be11fd92-c2c2-43ab-a5b7-c7085f10b778)

Wazuh is now getting configured and we just play the waiting game until it is ready

![Snag_4ef69a7](https://github.com/user-attachments/assets/6024217d-c012-414c-aac8-398a2095b39d)

The setup is now complete. Take note of the login credentials provided at the end of the install 

![Snag_4f6d60b](https://github.com/user-attachments/assets/850d05db-3637-4549-9cc4-58796ef752b3)

In order to get to the Wazuh dashboard, it’s going to be the local IP of the endpoint you installed it on

![Snag_4f945b3](https://github.com/user-attachments/assets/6b8406a2-c8c2-420f-832f-b1eb9859bf1f)

Once you put the IP in the URL and navigate to the dashboard, you are met with the login screen. Go ahead and put those provided credentials you got from the previous step and enter them in here. 

![Snag_4faac39](https://github.com/user-attachments/assets/3a6ba18a-60af-46be-ba93-bda0b93df1ac)

Once you login, you are not met with the Wazuh dashboard

![Snag_4fbaf22](https://github.com/user-attachments/assets/abe7ee27-f732-4525-bd66-7b95929edcb8)

I wanted to install an agent to talk back with the manager to start sending logs to it, so I navigated to Server Management>Endpoints Summary> then clicked on deploy new agent 

![Snag_4ff372f](https://github.com/user-attachments/assets/29a07cac-b8f1-4ce0-83de-f9f40e212202)


I am installing this on a Windows machine, so I just fill out the information required to get the PowerShell command at the end to install it

![Snag_502579a](https://github.com/user-attachments/assets/be68d367-3a11-4e93-81ff-4016edbd2d2e)

I now head back over to my Windows desktop and launch PowerShell as admin and load up the script

![Snag_5041586](https://github.com/user-attachments/assets/3c1a8a92-3015-4beb-8926-abd7f084e982)


I then started the service as well 

![Snag_5059abf](https://github.com/user-attachments/assets/da3218d6-bf05-4c8d-8b7b-f741baaa5e16)


Now that the service has started, I head back over to the Wazuh manager to see if the agent is checking in. 

Looks like the agent is successfully checking in with the Wazuh manager now 

![Snag_506f9f1](https://github.com/user-attachments/assets/3325e10e-ad08-4054-bdc7-cad904c0be6c)

I now let the agent sit on the desktop to start collecting telemetry about the desktop and it looks like its already logging Windows event logs by showing my login activity 

![Snag_50bb59c](https://github.com/user-attachments/assets/c9c09112-9c6e-4237-8d1e-5a5b34a302bb)

The agent is now reporting in a ton of data such as: Vulnerabilities, Registry key modifications, CIS benchmarks to harden the OS and even the MITRE ATT&CK Top tactics

![Snag_82e5f4d](https://github.com/user-attachments/assets/3b6330a5-2f9c-44e8-b5c5-9f9ce6f05eeb)


Looking at the events for registry key modifications, we can see there have been some registry keys that were deleted 

![Snag_8309c2d](https://github.com/user-attachments/assets/1b1a69e4-fda1-422a-a258-f5865e669a94)


Here is a screenshot that has more information about a specific row 

![Snag_831b175](https://github.com/user-attachments/assets/5842dd09-8a70-4c09-a140-80f004b6d3df)


We also can see vulnerabilities found on the machine 

![Snag_832808d](https://github.com/user-attachments/assets/9d63e527-59d0-45b6-823b-fbb224a9aeba)

We can also see events such as authentication failures and successful logins

![Snag_8344734](https://github.com/user-attachments/assets/3bd88344-ace8-4be1-9359-556af6385496)


Wazuh is an amazing tool and you can get really specific with it. I went ahead and modified the config file on the windows host machine (located at C:\Users\Your username here\Program Files x86\ossec-agent then look for the ossec.conf file) to look at specific directories for any type of changes. 

![Snag_123c83e4](https://github.com/user-attachments/assets/faeec9ee-6602-45bb-b6d6-7e93e6ca2e1c)

Now that the Desktop and Documents directory is being watched, lets change the syscheck time to report the alert much faster than the standard 12 hours. In this screenshot, I set the time to 120 seconds. 

![Snag_123f7436](https://github.com/user-attachments/assets/988a6884-26db-4a33-a41c-947ea896034f)

Now, lets create a txt file on our desktop and see the results in Wazuh. I named the txt file "Can you see this" 

![Snag_12404dae](https://github.com/user-attachments/assets/a69f70f1-acce-4717-9ee9-062026b69836)

Now, we head back over to our Wazuh manager to see the modification come in. Navigate to File integrity monitoring and select the events tab. As you can see, we can see the newly created txt document. 

![Snag_1241f207](https://github.com/user-attachments/assets/7f7eda83-1424-4a8b-ad13-8e72a80ecd11)

Now, let’s modify the file to see if Wazuh catches that as well. 

![Snag_1242a673](https://github.com/user-attachments/assets/e89e5152-59cf-42a7-8e7e-f42287ddaabc)

Now, let’s go back to Wazuh to see if it can find the file modification now. 

Looks like Wazuh did detect that as well!! 

![Snag_12443b7a](https://github.com/user-attachments/assets/013961e8-c754-44b3-ab2a-b7b4c049d687)

Now, let’s set up an integration to alert us. I will be using Slack for this project. 

First, you will need to create a Slack account. Once created create a channel called "Wazuh" for example. Once you do this, click on "See more preferences" then connected accounts. Once here click on App management page. 

![Snag_1252e12c](https://github.com/user-attachments/assets/5e6fdb2c-3697-41c2-a6e7-5dd521648e74)

Once you do this. Navigate to "Incoming Webhooks". From here, turn the feature on. Once on, take the Webhook URL and add it over to the Wazuh manager.

I went ahead and added the integration into the Wazuh manager. I am looking for specific rule.id's and a severity level to trigger. For exmaple, failed logins would trigger and then send back to Slack for an alert.  

![Snag_124612ab](https://github.com/user-attachments/assets/b8c12e9d-1ce6-4415-9ae9-62f28508e590)


Conclusion: I have successfully installed Wazuh manager on a Ubuntu OS and downloaded an agent onto a Windows desktop to check in and start sending logs to the manager. Moreover, I added specific directories to be watched on the host agent as well as modified the time it takes to send an alert to the Wazuh manager. In addition, I added Slack integration to alert me of different severity levels and rule id's that are triggering.
