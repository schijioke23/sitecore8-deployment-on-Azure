 
 How to deploy Sitecore 8.0 solution to Microsoft Azure Web App using Visual Studio

> **NOTE:** On Azure Web Apps, Sitecore does not support scaling out App Service Plan due to shared `WWWROOT` directory between instances. Sitecore application has certain types of data that requires persistence in the file system.

After developing a Sitecore solution in Visual Studio, it is possible to manually publish this solution to the Microsoft Azure Cloud Platform. This article provides a list of techniques that can be used to deploy a Sitecore solution to Microsoft Azure using Microsoft Visual Studio.

> **Important:** It is highly recommended that you get acquainted with the [Compute Hosting Options Provided by Azure](http://azure.microsoft.com/en-us/documentation/articles/fundamentals-application-models/) and [Microsoft Azure Fundamentals](http://www.microsoftvirtualacademy.com/colleges/Azure-fundamentals) before following the instructions in this article.


**Requirements:**
- A work or school account / Microsoft account and a Microsoft Azure subscription with the following Azure services enabled:
  - [Azure Web App](https://msdn.microsoft.com/en-us/library/azure/dn948515.aspx)
  - [Azure Storage](https://msdn.microsoft.com/en-us/library/azure/gg433040.aspx)
  - [Azure SQL Database](https://msdn.microsoft.com/en-us/library/azure/ee336279.aspx)
- Microsoft Visual Studio 2013 / 2015
- Microsoft Azure SDK 2.8.2 for .NET or newer
- Microsoft SQL Server Management Studio 2014 or newer
- MongoDB 2.6.1
- Sitecore® Experience Platform™ 8.0 rev. 160115 (8.0 Update-7) or higher

> **Note:** To download the latest version of the Microsoft Azure SDK and Tool for Visual Studio, follow this link: http://azure.microsoft.com/en-us/downloads/

##Instructions

The recommended approach to deploy a Sitecore solution to Microsoft Azure using Visual Studio is as follows:

1. Log in to the **Microsoft Azure Portal** using the https://portal.azure.com URL.
  
   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-01.png)
  
2. In the **Jumpbar**, click the **New** button, then select the **Web + Mobile** section and click the **Web App** button. The **Web App** blade appears.
   
   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-02.png)
   
3. In the **Web App** blade, fill in the **URL** field and configure the other section if needed, then click the **Create** button. 
 
   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-03.png)
 
4. In the **Startboard**, click on the **Web App** tile.

   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-04.png)

5. In the **Web App** blade, click the **All settings** button and select the **Application settings** section.
 
   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-05.png)
 
6. In the **Application settings** blade, configure the following groups and save the changes.
7. 
In the **General settings** group:
     + Set the **PHP version** switcher to the **Off** value. 
     + Set the **Platform** switcher to the the **64-bit** value.
     + Set the **Always On** switcher to the the **On** value.
     + \[Optional\] Set the **Remote debugging** switcher to the **On** value and select the Visual Studio version.
   
   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-06.png)
   
   - In the **Connection strings** group:
     + Add the `core`, `master`, `web`, `reporting` and `session` SQL Database connection strings.
     + Add the `analytics`, `tracking.live`, `tracking.history` and `tracking.contact` MongoDB connection strings.   

   ![](https://github.com/schijioke23/Sitecore-Azure-Content/raw/master/articles/media/how-to-deploy-sitecore-80-solution-to-microsoft-azure-web-app-using-visual-studio/AzurePortal-WebApp-07.png)
  
   > **Note:** For information on deploying Sitecore databases to Azure, see the section [How to deploy Sitecore databases to Azure SQL Database](how-to-deploy-sitecore-databases-to-azure-sql-database.md).
   
   ```xml
   Server=tcp:{server-name}.database.windows.net,1433;Database=Sitecore.Core;User ID={server-admin-login}@{server-name};Password={password};Trusted_Connection=False;Encrypt=True
   Server=tcp:{server-name}.database.windows.net,1433;Database=Sitecore.Master;User ID={server-admin-login}@{server-name};Password={password};Trusted_Connection=False;Encrypt=True
   Server=tcp:{server-name}.database.windows.net,1433;Database=Sitecore.Web;User ID={server-admin-login}@{server-name};Password={password};Trusted_Connection=False;Encrypt=True
   Server=tcp:{server-name}.database.windows.net,1433;Database=Sitecore.Reporting;User ID={server-admin-login}@{server-name};Password={password};Trusted_Connection=False;Encrypt=True
   Server=tcp:{server-name}.database.windows.net,1433;Database=Sitecore.Session;User ID={server-admin-login}@{server-name};Password={password};Trusted_Connection=False;Encrypt=True
   
   mongodb://{user-name}:{password}@{thehost}/sitecore_analytics
   mongodb://{user-name}:{password}@{thehost}/sitecore_tracking_lives
   mongodb://{user-name}:{password}@{thehost}/sitecore_tracking_historys
   mongodb://{user-name}:{password}@{thehost}/sitecore_tracking_contact 
   ```
