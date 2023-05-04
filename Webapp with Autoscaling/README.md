# Implementing WebApp with Autoscaling

In this Project, I have created a 'Hello World' application on WebApp and configured Autoscaling for this application.

# Project Details
 - The services that were used during the course of this Projects are as follows:
     - Powershell 
     - App Service
     - Deployment Slots
     - Autoscaling the App Service Plan by Scaling Out 
- Please refer to the DOC file for a detailed report.
- JSON Templates for Virtual Network.

# Steps

- Using the App Service created WebApp with the following details:
   - Name:arsenalfootballclub.azurewebsites.net
   - resource group (az104-09a-rg1
   - runtime stack is PHP 8.0   
   - Linux OS
   - app service plan that I have taken is Standard S1 (100 ACU, 1.75 GB Memory and 1 vCPU).
   
  
  ![1](https://user-images.githubusercontent.com/106948902/236281797-1a60d2cc-e0bc-4c1d-b9cd-b6f10228cfdf.jpg)
 

- WebApp Succesfully Deployed 
 
 
  ![2](https://user-images.githubusercontent.com/106948902/236281877-cd484dd6-c0af-4328-baef-46565f911fea.jpg)

   
- Created a New Deployment slot (Staging) to a pre deployment from Production

  ![4](https://user-images.githubusercontent.com/106948902/236282009-043b006d-590e-4950-bc54-962e78868545.jpg)

- Configured local repository on the Staging Slot, configured the credentials/FTPS Credentials, GIT Clone URI, branch

  ![5](https://user-images.githubusercontent.com/106948902/236282145-7670d489-bf58-4279-b9bc-f5e6e45d31e4.jpg)

- Cloned and Deployed the application which is present in GitHub, to the Staging Slot using PowerShell.

  ![15](https://user-images.githubusercontent.com/106948902/236282426-18f93993-a6a1-4d55-8d75-56fb1b830b03.png)

- Swapped the Staging slot with Deployment slot to make our application available on the 'arsenalfootballclub.azurewebsites.net' Domain Name.

  ![8](https://user-images.githubusercontent.com/106948902/236282525-8a2b072e-2e81-4b4b-96aa-8989a07f2294.jpg)

  ![9](https://user-images.githubusercontent.com/106948902/236282751-b3acfdbd-b953-4ed6-9109-f4fa2ab9ef04.jpg)

- Created Autoscaling rules based on metrics to scale out the WebApp. 

  ![11](https://user-images.githubusercontent.com/106948902/236282604-aa0ccf78-9e4f-4ef7-95e6-8e708275909d.jpg)

  ![12](https://user-images.githubusercontent.com/106948902/236282625-3de893cf-28b1-4d4a-a544-517fa45d7deb.jpg)

- Finally, Testing the autoscale rule created using the PowerShell commands.

$rgName = 'az104-09a-rg1' <br>
$webapp = Get-AzWebApp -ResourceGroupName $rgName <br>
while ($true) { Invoke-WebRequest -Uri $webapp.DefaultHostName }

   
# Troubleshooting

- While creating the Autoscaling Rule to scale out the WebApp, I was notified with the following error error 'microsoft.insights service is not registered'. 

   ![17](https://user-images.githubusercontent.com/106948902/236285615-cf3cdb0a-e89a-47ca-91e2-466fe5f02454.jpg)


- To resolve this eror, In the Resource Provider section of the Subcription, I looked for the microsoft.insights resource and registered this service.
    
- After registering the service, I was able to add the scale out rule.

   ![image](https://user-images.githubusercontent.com/106948902/236286457-53848c27-6de5-46e4-812d-09490d29a887.png)

# Conclusion

I have succesfully implemented WebApp using the App Service, created Staging Deployment slot to validate app changes before swapping with Production, automated the scale out procedure for the WebApp based on CPU Metric, if in case the Application faces heavy traffic load and tested these rules for the WebApp using PowerShell commands. 

