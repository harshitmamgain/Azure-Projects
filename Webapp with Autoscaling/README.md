# Implementing WebApp with Autoscaling

In this project, I created a 'Hello World' application on Azure App Service and configured autoscaling to ensure optimal performance and availability. This included setting up an autoscaling rule based on CPU percentage, allowing the application to automatically scale-out as needed to handle increased traffic and demand. These measures help to ensure a seamless user experience and prevent potential downtime during periods of high traffic or demand.

# Project Details
 - The services that were used during the course of this Projects are as follows:
     - Powershell 
     - App Service
     - GitHub
     - Deployment Slots
     - Autoscaling the App Service Plan by Scaling Out 
   

# Steps

- Using the App Service created WebApp with the following details:
   - Name: arsenalfootballclub.azurewebsites.net
   - resource group: az104-09a-rg1
   - Runtime Stack: PHP 8.0   
   - OS: Linux
   - App Service Plan: Standard S1 (100 ACU, 1.75 GB Memory and 1 vCPU)
   
  
  ![1](https://user-images.githubusercontent.com/106948902/236281797-1a60d2cc-e0bc-4c1d-b9cd-b6f10228cfdf.jpg)
 

- WebApp has been successfully deployed and is now accessible using the following domain name: 'arsenalfootballclub.azurewebsites.net'. This ensures that users can access the latest version of the application.
 
 
  ![2](https://user-images.githubusercontent.com/106948902/236281877-cd484dd6-c0af-4328-baef-46565f911fea.jpg)

   
- Created a New Deployment slot called Staging. By creating a new deployment slot called "Staging," the application now has a dedicated environment for testing its functionality before releasing it to users. This helps ensure a smooth user experience and reduces the risk of potential issues.

  ![4](https://user-images.githubusercontent.com/106948902/236282009-043b006d-590e-4950-bc54-962e78868545.jpg)

- In the Staging slot, I have configured the local repository and set up the necessary credentials and FTPS credentials. Additionally, I have configured the GIT Clone URI and specified the relevant branch for the deployment.

  ![5](https://user-images.githubusercontent.com/106948902/236282145-7670d489-bf58-4279-b9bc-f5e6e45d31e4.jpg)

- Using PowerShell, I have successfully cloned the application from GitHub and deployed it to the Staging slot. This allows us to test the application's performance and functionality in a dedicated environment before making it available to users. I have used the following commands:

  PS /home/harshit> git clone https://github.com/Azure-Samples/php-docs-hello-world <br>

  PS /home/harshit> Set-Location -Path $HOME/php-docs-hello-world/ <br>

  PS /home/harshit/php-docs-hello-world> git remote add arsenalfootballclub https://arsenalfootballclub-staging.scm.azurewebsites.net:443/arsenalfootballclub.git <br>

  PS /home/harshit/php-docs-hello-world> git push arsenalfootballclub master  

  ![15](https://user-images.githubusercontent.com/106948902/236282426-18f93993-a6a1-4d55-8d75-56fb1b830b03.png)

- After testing and verifying the application's functionality in the Staging slot, I swapped it with the Deployment slot, making the application available on the 'arsenalfootballclub.azurewebsites.net' domain name. This ensures that users can access the latest version of the application with minimal disruption.

  ![8](https://user-images.githubusercontent.com/106948902/236282525-8a2b072e-2e81-4b4b-96aa-8989a07f2294.jpg)

- Application is in the Producation Deployment slot and is available to everyone.  
  
  ![9](https://user-images.githubusercontent.com/106948902/236282751-b3acfdbd-b953-4ed6-9109-f4fa2ab9ef04.jpg)
- To ensure optimal performance and availability, I have set up autoscaling rules based on relevant metrics, allowing the WebApp to automatically scale out as needed. This helps to maintain a consistent user experience and prevents potential downtime during periods of high traffic or demand.

- The Scaling rule is as follows 
  - Metric Source - ASP-az10409arg1-b779
  - Metric Namespace - Standard Metrics
  - Metric Name - CPU Percentage
  - Operator - Greater than
  - Metric threshold to trigger action – 10 (at what metric or value should the action be triggered at)
  - Duration – 1 Minute
  - Time Grain – Maximum
  - Time Aggregation – Maximum

- Action
  - Operation – Increase count by
  - Cool Down – 5 minutes
  - Instance Count – 1
  
- The Minimum instances are set to 1, Maxminum instances are set to 2 and the Default Instances are set to 1.
 
The autoscaling rule that was created is set to trigger a scale-out action when the 'ASP-az10409arg1-b779' app service plan exceeds a maximum CPU percentage of 10. The action to be taken in this case is to increase the count by 1, allowing the WebApp to scale-out and handle increased traffic and demand. 


  ![11](https://user-images.githubusercontent.com/106948902/236282604-aa0ccf78-9e4f-4ef7-95e6-8e708275909d.jpg)

  ![12](https://user-images.githubusercontent.com/106948902/236282625-3de893cf-28b1-4d4a-a544-517fa45d7deb.jpg)

- As a final step, I am testing the autoscaling rule that was created using PowerShell commands. This ensures that the WebApp can handle increased traffic and usage, and that the autoscaling rules are functioning as intended. Any issues identified during testing can be addressed before the application is made available to users, ensuring a seamless experience.

$rgName = 'az104-09a-rg1' <br>
$webapp = Get-AzWebApp -ResourceGroupName $rgName <br>
while ($true) { Invoke-WebRequest -Uri $webapp.DefaultHostName }

   
# Troubleshooting

- During the process of creating the autoscaling rule to scale out the WebApp, I received an error notification stating that the 'microsoft.insights' service was not registered. This indicates that the required service is not currently available, which may prevent the autoscaling rule from functioning as intended. I investigated this issue and took the following steps to resolve it.

   ![17](https://user-images.githubusercontent.com/106948902/236285615-cf3cdb0a-e89a-47ca-91e2-466fe5f02454.jpg)


- To resolve the error related to the 'microsoft.insights' service not being registered, I navigated to the Resource Provider section of the Subscription and located the 'microsoft.insights' resource. I then registered this service, which should allow the autoscaling rule to function as intended. I will now retest the autoscaling rule to confirm that the error has been resolved.
    
- Following the successful registration of the 'microsoft.insights' service, I was able to add the required scale out rule to the WebApp. This ensures that the application can automatically adjust its resources to accommodate increased traffic and demand, providing a seamless experience for users.

   ![image](https://user-images.githubusercontent.com/106948902/236286457-53848c27-6de5-46e4-812d-09490d29a887.png)


# Conclusion

 I have successfully implemented the WebApp using the App Service, which includes a Staging Deployment slot to validate any app changes before swapping with Production. Additionally, I have automated the scale-out procedure for the WebApp based on CPU Metric, ensuring the application can handle increased traffic and demand without impacting user experience. I have tested these rules for the WebApp using PowerShell commands, confirming their successful implementation.

