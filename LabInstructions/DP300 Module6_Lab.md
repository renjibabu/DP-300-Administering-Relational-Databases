# Lab 6 – Automate Resources

 

**Estimated Time**: 60 minutes

**Pre-requisites**: A SQL login in the Azure database AdventureWorks has been created to allow for maintenance purposes

This lab can be performed from a web browser with access to the Azure portal.

Note: the Microsoft.Insights module needs to be added to your subscription in order to complete this lab. You can register by completing the following steps. 

From the Azure portal, click on the cloud shell icon on the top right of the portal.

![A picture containing racket, drawing, ball, woman Description automatically generated](images/dp-3300-module-66-lab-01.png)

A shell will open at the bottom of the screen. Click on PowerShell as shown below.

![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-02.png)


You may be prompted to create a storage account. Click Create Storage. 

![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-03.png)

Paste in the following command: 

register-AzResourceProvider -ProviderNamespace Microsoft.Insights

![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-04.png)

 

**Lab files**: The files for this lab are in the D:\LabFiles\Automate Resources folder.

# Lab overview

The students will take the information gained in the lessons and the case study to configure and subsequently implement automate processes within AdventureWorks. 

# Lab objectives

After completing this lab, you will be able to:

1. Deploy an Azure resource from a GitHub Quickstart template

2. Schedule maintenance jobs and configure notifications

3. Configure multi-server automation

4. Configure performance metric related notifications

5. Configure notifications based on resources

6. Deploy an Azure Automation Runbook to perform index maintenance in an Azure SQL Database

# Scenario

You have been hired as a Senior Data Engineer to help automate day to day operations of database administration. This automation is to help ensure that the databases for AdventureWorks continue to operate at peak performance as well as provide methods for alerting based on certain criteria. AdventureWorks utilizes SQL Server in both Infrastructure as a Service and Platform as a Service offerings. 

 

# Exercise 1: Deploy an Azure Quickstart Template 

Estimated Time: 30 minutes

Individual Exercise

The main task for this exercise is as follows:

1. Deploy an Azure resource from a GitHub Quickstart template

2. Configure performance metric related notifications

3. Deploy an Azure Automation Runbook to perform index maintenance in an Azure SQL Database

## Task 1: Deploy an Azure SQL Database

1. Navigate to the following GitHub using a web browser. 

    [https://github.com/Azure/azure-quickstart-templates/tree/master/201-sql-database-transparent-encryption-create](https://github.com/Azure/azure-quickstart-templates/tree/master/201-sql-database-transparent-encryption-create)

 
    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-05.png)

    Click on azuredeploy.json, and review the file. 


2. Navigate back the above link, and click on the Deploy to Azure button. You may be prompted to login to the Azure portal. Login with your supplied credentials.


3. You will see the following screen. In order to deploy this template, you need to complete the blank fields.


    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-06.png) 

    In the Resource Group field, click “Create New” and type DP300-Lab06. In the SQL Administrator login field, type **labadmin**. For the password field, type the password **Azur3Pa$$**. Click on the check box next to “I agree to the terms and conditions” and then click purchase. 


4. After you click Purchase. Your deployment will begin. You can track the status of your deployment by clicking the bell (highlighted in the screenshot below) and then clicking on the Deployment in progress link in the Notifications pane.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-07.png)


    Your deployment will take approximately 5-10 minutes to deploy. If you have clicked on the link above, you will be able to track your deployment. 

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-08.png)

5. Upon completion, the screen will update with a link to your newly created resources. 

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-09.png)


    Click on the Go to resource link. You will be taken to the Azure Resource Group your deployment just created. Make note of the name of your SQL server, as you will use it in the next exercise.

    ![A screenshot of a social media post Description automatically generated](images/dp-3300-module-66-lab-10.png)

 

# Exercise 2: Configure Performance Metrics Based Alerts

Estimated Time: 30 minutes

Individual Exercise

The main task for this exercise is as follows:

1. Configure performance metric related notifications

## Task 1: Creating an alert when CPU exceeds an average of 80 percent.

1. Navigate back to portal.azure.com. You may need to login again. In the search bar at the top of the Azure Portal, type SQL, and click on SQL databases. Click on the database name.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-11.png)


2. On the main blade for the sample-db-with-tde database, navigate down to the monitoring section 

3. Click on Alerts

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-12.png)


4.  Click on New Alert Rule.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-13.png)

 

5. You will notice that the resource is already populated for you with the database you created. Under the Condition section, click Select Condition.

    ![A screenshot of a social media post Description automatically generated](images/dp-3300-module-66-lab-14.png)

6. In the Configure signal logic slide out menu, select CPU Percentage. 

    ![Picture 14](images/dp-3300-module-66-lab-15.png)


7. Supply a threshold value of 80. Click Done.

    ![Picture 15](images/dp-3300-module-66-lab-16.png)

8. Under Action Groups (optional) section, click Select Action Group 

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-17.png)

9. In the fly out for Action Group, Click Create action group.


    ![A picture containing table, knife Description automatically generated](images/dp-3300-module-66-lab-18.png)

    In the Action Group screen, type emailgroup in the Action group name field.


    ![A screenshot of a social media post Description automatically generated](images/dp-3300-module-66-lab-19.png)

 
10. Then click on the notifications tab.

    ![Picture 2059024190](images/dp-3300-module-66-lab-20.png)


11. Select Email/SMS message/Push/Voice and enter the name DemoLab. In the flyout screen on the right, click the check box next to email and click OK. Then click on the Review and Create button, and then click Create on the Create Action group screen.


    From the Create alert rule screen, add an Alert rule name of DemoAlert, and then click Create Alert Rule as show below.
 

    ![A screenshot of a computer Description automatically generated](images/dp-3300-module-66-lab-21.png)

 


# Exercise 3: Deploy an Automation Runbook


Estimated Time: 30 minutes

Individual Exercise

The main task for this exercise is as follows:

1. Deploy a maintenance task script.

2. Deploy an Azure Automation Runbook to perform index maintenance in an Azure SQL Database

## Task 1:Deploy an Automation Runbook to rebuild indexes in an Azure SQL Database.

1. From the lab virtual machine, start a browser session and navigate to [https://portal.azure.com](https://portal.azure.com/). Provide appropriate credentials. 

    ![Picture 2](images/dp-3300-module-66-lab-22.png)

2. In the Azure Portal in the search bar type Automation and then click on Automation Accounts

    ![Picture 2075709555](images/dp-3300-module-66-lab-23.png)

    Click on the + Add button in the portal.
 
    ![Picture 1590905270](images/dp-3300-module-66-lab-24.png)

3. Create your automation account

    ![Picture 757014512](images/dp-3300-module-66-lab-25.png)


    Name: **DP3006Lab06**

    Resource Group: Use the resource group you created in Lab 2. **DP300-Lab02**

    Location: Use the region in which you created your Azure SQL server in Lab 2

    Click Create. Your automation account should deploy in 1-3 minutes. 


4. Navigate to the **github** page for AdaptativeIndexDefragmentation. [https://github.com/microsoft/tigertoolbox/blob/master/AdaptiveIndexDefrag/usp_AdaptiveIndexDefrag.sql](https://github.com/microsoft/tigertoolbox/blob/master/AdaptiveIndexDefrag/usp_AdaptiveIndexDefrag.sql)

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-26.png)

 
    Click on Raw. This will provide the code in a format where you can copy it. Select all of the text and copy it to your clipboard. 


5. In the Azure Portal, navigate back to your database and click on the Query Editor as shown below.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-27.png)

6. You will be prompted for credentials to login to your database. Use the credentials you created in Exercise 1.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-28.png)


    You may receive an error that a firewall rule needs to be created as shown below.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-29.png)

    Click on the blue Set server firewall link at the end of the error message as shown above. The server firewall screen will come up. Click Add client IP as highlighted below.


    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-30.png)

    Click the Save button to save the firewall configuration

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-31.png)

    After you see the success message above, click on the link to Query editor (outlined in red in the above image) above the firewall settings pane. 


    When you return to the query editor, click Ok, to login to your database. Paste the text you copied in Step 2 into the Query 1 pane. 

    ![A screenshot of a social media post Description automatically generated](images/dp-3300-module-66-lab-32.png)


    Delete the USE msdb and GO statements on lines 5 and 6 of the query (that are highlighted in the above screenshot) , and then click run. 

    ![A screenshot of a social media post Description automatically generated](images/dp-3300-module-66-lab-33.png)


    The query will take around 20 seconds to complete. 


7. Once into the Azure portal, expand the left menu and click on All Services within the main Azure panel. 

    ![Picture 18](images/dp-3300-module-66-lab-34.png)

8. Type automation within the search field. Click on Automation Accounts. 

    ![Picture 21](images/dp-3300-module-66-lab-35.png)


    Identity the automation account that has been created in your subscription and click on it.


    ![Picture 1165377632](images/dp-3300-module-66-lab-36.png)

9. Select Modules from the Shared Resources section of the Automation blade. 

    ![Picture 1267754120](images/dp-3300-module-66-lab-37.png)

10. Click on Browse Gallery

    ![Picture 974424449](images/dp-3300-module-66-lab-38.png)


11. Search for sqlserver within the Gallery

    ![Picture 1043266059](images/dp-3300-module-66-lab-39.png)


12. Click on the SqlServer text which will direct to the next screen. Click on Import
    ![Picture 31](images/dp-3300-module-66-lab-40.png)

13.  Click on Ok in the bottom corner of the screen in order to import the module. This will import the PowerShell module into your Automation account.
    ![Picture 32](images/dp-3300-module-66-lab-41.png)


14. You will need to create a credential to securely login to your database. From the Automation Account blade navigate to the Shared Resources Section and click Credentials.

    ![Picture 1940038127](images/dp-3300-module-66-lab-42.png)


    Click + Add a Credential, and then create a credential as shown below. Name the credential SQLUser and use the labadmin username and Azur3Pa$$ for the password. Click create.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-43.png)


15. Scroll to the Process Automation section of the Automation account blade and click on Runbooks and then Create a runbook.

    ![Picture 568038330](images/dp-3300-module-66-lab-44.png)

16. Supply a runbook name of IndexMaintenance and a runbook type of Powershell. You can supply a short description of your choosing. Click create once finished. 

    ![Picture 1283377310](images/dp-3300-module-66-lab-45.png)

    Once the runbook has been created, the process should drop you directly into the runbook.   
‎

17. Copy the code below into the runbook. Edit the $AzureSQLServerName variable to reflect the name of your Azure SQL server. You can get this value from the overview screen of your Azure SQL Database as shown below.

    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-46.png)


    Copy the name of the server including the .database.windows.net domain suffix. Using Windows Explorer right click on the Open the DP300-Lab-Module-6.ps1 file from the D:\LabFIles\Automate Resources folder and click edit. The PowerShell IDE will open.


    ![A screenshot of a cell phone Description automatically generated](images/dp-3300-module-66-lab-47.png)


    On Line 1 of the file paste in your server name. Select all of the text and copy it to your clipboard. 


18. Navigate back to your automation runbook, and paste in the PowerShell code you copied from the PowerShell IDE in step 17. Then click Save and then click Publish

    ![Picture 679031903](images/dp-3300-module-66-lab-48.png)


19. Click Yes when prompted to over-write any previously published versions. 

    ![Picture 36](images/dp-3300-module-66-lab-49.png)

20. Next you will schedule the runbook to execute on a regular basis. Click on Schedules in the left hand navigation menu. Then click on Add a schedule at the top. 

    ![Picture 1181869969](images/dp-3300-module-66-lab-50.png)

21. Click on Link a schedule to your runbook. 

22. Select Create a new schedule. 

    ![Picture 2105012659](images/dp-3300-module-66-lab-51.png)

23. Supply a descriptive schedule name and a description if desired. 

24. Specify the start time of 4:00AM of the following day and in the Eastern Time zone. Configure the reoccurrence for every 1 days. Do not set an expiration. 

    ![Picture 39](images/dp-3300-module-66-lab-52.png)

25.  Click Ok. 

26. The schedule is now linked to the runbook. 

    ![Picture 218516936](images/dp-3300-module-66-lab-53.png)

 

 

 

 

 
