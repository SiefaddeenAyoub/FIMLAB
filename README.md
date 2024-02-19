# SIEM Azure Sentinel

## Objective

 I set up Azure Sentinel (SIEM) and connected it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. We will use a custom PowerShell script to look up the attacker's Geolocation information and plot it on the Azure Sentinel Map!

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Used custom PowerShell script to extract security events from Windows Event Viewer which was then delivered to a third-party API to break down the geolocation data.
- Proficiency in analyzing and interpreting network logs.
- Configured Azure Sentinel workbook to display global attack data (Brute Force Attacks) on the world map depending on attack location.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- VM
- IPEGEOLOCATION.IO
- Microsoft Azure

## Steps
1. First we are creating a VM in Microsoft Azure, with it simply being our Honey Pot.
<img src="https://i.imgur.com/QlbB6rm.png"/>

2. Next we are putting in the information needed for our VM including our region and login details.
<img src="https://i.imgur.com/EgoAEs3.png"/>

3. Next we are going to the Create Network Security Group and creating a Firewall that will be very vulnerable to brute force attacks, to showcase what we are attempting during this lab.
<img src="https://i.imgur.com/Bl0NLjO.png"/>

4. Next we are creating a Log Analytics Workspace to injust logs from the VM.
<img src="https://i.imgur.com/QSDtwVa.png"/>

5. Now we have to go to the Microsoft Defender For cloud in the Environment settings in order to enable the ability to gather logs from the VM into the Log Analytics Workspace.
<img src="https://i.imgur.com/MM40l8b.png"/>

6. Now we are connecting our Log Analytics workspace to the VM.
<img src="https://i.imgur.com/odzxKux.png"/>

7. Using Microsoft Sentinel SIEM to visualize the attack data.
<img src="https://i.imgur.com/sUGBuzG.png"/>

8. Next we are connecting the VM on a remote desktop using the provided IP address and using the login information that we set in step 2.
<img src="https://i.imgur.com/RqbPnpW.png"/>

9. We failed the first attempt when logging in so that when we pull up the security logs in the event viewer on the VM we can see that it saved the failed login, but now we are logging into the VM.
<img src="https://i.imgur.com/vqHq6In.png"/>

10. Next we pulled a Powershell script that was already provided and the only thing we changed was our custom ipe geolocation number in order to get all the brute force attacks' exact location.
<img src="https://i.imgur.com/DCQa5o1.png"/>

11. Powershell looks through the event viewer and sends information to API geolocation gets all the named info and sends it back to the Powershell.
<img src="https://i.imgur.com/wTUtP0G.png"/>

12. Next we create a custom log using the failed RDP data from the VM. (We got this data from the 2-3 failed login attempts that we made while trying to log into the Remote Desktop)
<img src="https://i.imgur.com/9icDTCy.png"/>

13. Here we are looking at the security events that are normally in the VM's event viewer/security event but since we had the VM connect to the log analytics workspace, information now pops up in our log analytics workspace. As shown in the image you can see the 3 failed login attempts.
<img src="https://i.imgur.com/PxtG97F.png"/>

14. After waiting 20 minutes for the VM to connect to the log analytics workspace we are able to get the raw data that was in the Failed RDP data, which includes the fake samples as well as our 3 attempting wrong logins (WE DONT HAVE TO WORRY ABOUT THE SAMPLES POPPING UP ON THE MAP BECAUSE WHEN WE EXTRACT THE DATA WE CAN MAKE IT TO WHERE IT DOES NOT PULL ANY INFORMATION THAT HAS SAMPLE IN THE LINE)
<img src="https://i.imgur.com/3O8C3nS.png"/>

15. Now we are extracting fields from the log for longitude, latitude, Country, state, etc.
<img src="https://i.imgur.com/KxXDi5I.png"/>

16. After extracting our data, this is what our columns look like.
<img src="https://i.imgur.com/wTs9SQP.png"/>

17. After failing another login on the remote desktop we get a new log that shows the information with our extracted data, our VM has not reached the hackers of the world yet so we are just waiting.
<img src="https://i.imgur.com/x6St3Ga.png"/>

18. While we wait for our VM to reach the hackers of the world we will set up the world map in sentinel using the longitude and latitude.
<img src="https://i.imgur.com/ocS1pfU.png"/>

19. After 4 hours of letting the VM run and the Powershell script running the hackers of China finally started attempting to Brute force attack our VM.
<img src="https://i.imgur.com/x3FdfgV.png"/>

20. If we open our VM again and look at the Powershell script we can see the Chinese attempting to log in.
<img src="https://i.imgur.com/A63uibj.png"/>

21. After a couple more hours pass by we can see that Taiwan has joined in on the action.
<img src="https://i.imgur.com/RXUrv5s.png"/>

22. We left the VM running overnight and here are the results.
<img src="https://i.imgur.com/dDDA0Et.png"/>

23. Something you can definitely take away from doing this lab is to avoid using easily guessable passwords cause as you see in the screenshot administrator is the most guessed password!
<img src="https://i.imgur.com/QelgnuX.png"/>


Thanks for experiencing my Lab with me! 





Credits go to: Josh Madakor on YouTube.
