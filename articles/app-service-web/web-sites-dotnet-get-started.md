<properties
	pageTitle="Create an ASP.NET web app in Azure App Service | Microsoft Azure"
	description="This tutorial shows you how to create an ASP.NET web project in Visual Studio 2013 and deploy it to a web app in Azure App Service."
	services="app-service\web"
	documentationCenter=".net"
	authors="tdykstra"
	manager="wpickett"
	editor="jimbe"/>

<tags
	ms.service="app-service-web"
	ms.workload="web"
	ms.tgt_pltfrm="na"
	ms.devlang="dotnet"
	ms.topic="hero-article"
	ms.date="03/02/2015"
	ms.author="tdykstra"/>

# Create an ASP.NET web app in Azure App Service

> [AZURE.SELECTOR]
- [.Net](web-sites-dotnet-get-started.md)
- [Node.js](web-sites-nodejs-develop-deploy-mac.md)
- [Java](web-sites-java-get-started.md)
- [PHP - Git](web-sites-php-mysql-deploy-use-git.md)
- [PHP - FTP](web-sites-php-mysql-deploy-use-ftp.md)
- [Python](web-sites-python-ptvs-django-mysql.md)

## Overview

This tutorial shows how to deploy an ASP.NET web application to a [web app in Azure App Service](app-service-web-overview.md) by using Visual Studio 2015. The tutorial assumes that you are an ASP.NET developer who has no prior experience with using Azure. On completing the tutorial, you'll have a simple web application up and running in the cloud.

The following illustration shows the completed application:

![Web app running in Azure](./media/web-sites-dotnet-get-started/GS13deployedsite.png)

You'll learn:

* How to create a new App Service web app while you create a new web project in Visual Studio.
* How to deploy a web project to an App Service web app by using Visual Studio.
* How to use the [Azure Portal](/overview/preview-portal/) to monitor and manage your web app.

At the end of the tutorial, the [Next steps](#next-steps) section provides links to other tutorials that go into more depth about how to use Azure App Service.

> [AZURE.NOTE] Help us shape the scope and approach of this tutorial -- if there are other topics you'd like to see covered here in a getting-started tutorial leave feedback in a [Disqus comment](#comments) at the end of the tutorial.

[AZURE.INCLUDE [prereqs](../../includes/app-service-web-dotnet-get-started-prereqs.md)]

## Create a project and a web app

Your first step is to create a web project in Visual Studio and a web app in Azure App Service. When that's done, you'll deploy the project to the web app to make it available on the Internet. 

The diagram illustrates what you're doing in the create and deploy steps.

![Create and deploy](./media/web-sites-dotnet-get-started/Create_App.png)

1. Open Visual Studio 2015.

2. Click **File > New > Project**.

3. In the **New Project** dialog box, click **Visual C# > Web > ASP.NET Web Application**. (If you prefer, you can choose **Visual Basic**.)

3. Make sure that **.NET Framework 4.5.2** is selected as the target framework.

4.  [Azure Application Insights](../application-insights/app-insights-overview.md) monitors your web app for availability, performance, and usage. The **Add Application Insights to Project** check box is selected by default the first time you create a web project after installing Visual Studio. Clear the check box if it's selected but you don't want to try Application Insights.

4. Name the application **MyExample**.

5. Click **OK**.

	![New Project dialog box](./media/web-sites-dotnet-get-started/GS13newprojdb.png)

5. In the **New ASP.NET Project** dialog box, select the **MVC** template.

7. Click **Change Authentication**.

	![New ASP.NET Project dialog box](./media/web-sites-dotnet-get-started/GS13changeauth.png)

6. In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.

	![No Authentication](./media/web-sites-dotnet-get-started/GS13noauth.png)

	The application that you're creating for this tutorial is a simple one that doesn't support user log-in.

5. In the **Microsoft Azure** section of the **New ASP.NET Project** dialog box, make sure that **Host in the cloud** is selected and that **App Service** is selected in the drop-down list.

	![New ASP.NET Project dialog box](./media/web-sites-dotnet-get-started/GS13newaspnetprojdb.png)

	These settings specify that Visual Studio will create an Azure web app for your web project.

6. Click **OK**.

5. If you haven't already signed in to Azure, Visual Studio prompts you to do so. Sign in with the ID and password of the account that you use to manage your Azure subscription.

	When you're signed in, the **Create App Service** dialog box asks you what resources you want to create.

	![Signed in to Azure](./media/web-sites-dotnet-get-started/configuresitesettings.png)

3. In the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain. For example, you can name it MyExample with numbers to the right to make it unique, such as MyExample810. If a default web name is created for you, it will be unique and you can use that.

	If someone else has already used the name that you enter, you'll see a red exclamation mark to the right instead of a green check mark, and you'll need to enter a different name.

	Azure will use this name as the prefix for your application's URL. The complete URL will consist of this name plus *.azurewebsites.net* (as shown next to the **Web App Name** text box). For example, if the name is `MyExample810`, the URL will be `myexample810.azurewebsites.net`. The URL has to be unique.

6. Next to the **Resource Group** box, click **New**, and then enter "MyExample" or another name if you prefer. 

	This combo box lets you select an existing resource group or create a new one by typing in a name that is different from any existing resource group in your subscription.

	A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.	For a tutorial it's generally best to create a new resource group because that will make it easy to delete in one step any Azure resources that you create for the tutorial. For more information, see [Azure Resource Manager overview](../resource-group-overview.md)

4. Click the **New** button next to the **App Service Plan** drop-down.

	![Create App Service dialog](./media/web-sites-dotnet-get-started/createas.png)

	The screen shot shows sample values for **Web App Name**, **Subscription**, and **Resource Group** -- your values will be different.

	In the following steps you create an App Service plan for the new resource group. An App Service plan specifies the compute resources that your API app runs on. For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs. For more information, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).

5. In the **Configure App Service Plan** dialog, enter "MyExamplePlan" or another name if you prefer.

5. In the **Location** drop-down list, choose the location that is closest to you.

	This setting specifies which Azure datacenter your app will run in. For this tutorial, you can select any region and it won't make a noticeable difference. But for a production app, you want your server to be as close as possible to the clients that are accessing it in order to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).

5. In the **Size** drop-down, click **Free**.

	For this tutorial, The free pricing tier will provide sufficient performance.

6. In the **Configure App Service Plan** dialog, click **OK**.

	![Configure App Service dialog](./media/web-sites-dotnet-get-started/configasp.png)

7. In the **Create App Service** dialog box, click **Create**.

	![Create App Service dialog box](./media/web-sites-dotnet-get-started/clickcreate.png)

	In a short time, usually less than a minute, Visual Studio creates the web project and the web app.  

	The **Solution Explorer** window shows the files and folders in the new project.

	![Solution Explorer](./media/web-sites-dotnet-get-started/solutionexplorer.png)

	The **Azure App Service Activity** window shows that the web app has been created.

	![Web app created](./media/web-sites-dotnet-get-started/GS13sitecreated1.png)

	And you can see the web app in **Cloud Explorer**.

	![Web app created](./media/web-sites-dotnet-get-started/siteinse.png)

## Deploy the project to the web app

In this section you deploy web project to the web app, as illustrated in step 2 of the diagram.

![Create and deploy](./media/web-sites-dotnet-get-started/Create_App.png)

1. In **Solution Explorer**, right-click the project, and choose **Publish**.

	![Choose Publish](./media/web-sites-dotnet-get-started/choosepublish.png)

	In a few seconds, the **Publish Web** wizard appears. The wizard opens to a *publish profile* that has settings for deploying the web project to the new web app. If you wanted to deploy to a different web app, you could click the **Profile** tab to create a different profile. For this tutorial, you'll accept the settings that deploy to the web app that you created earlier.

8. On the **Connection** tab of the **Publish Web** wizard, click **Next**.

	![Successfully validated connection](./media/web-sites-dotnet-get-started/GS13ValidateConnection.png)

	The next tab is the **Settings** tab. Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). The tab also offers several **File Publish Options**:

	* Remove additional files at destination
	* Precompile during publishing
	* Exclude files from the App_Data folder

	For this tutorial you don't need any of these. For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).

10. On the **Settings** tab, click **Next**.

	![Settings tab](./media/web-sites-dotnet-get-started/GS13SettingsTab.png)

	The **Preview** tab is next. Here you have an opportunity to see what files are going to be copied from your project to the API app. When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied. If you want to see a list of what will be copied, you can click the **Start Preview** button.

11. On the **Preview** tab, click **Publish**.

	![Preview tab](./media/web-sites-dotnet-get-started/GS13previewoutput.png)

	When you click **Publish** Visual Studio begins the process of copying the files to the Azure server. This may take a minute or two.

	The **Output** and **Azure App Service Activity** windows show what deployment actions were taken and report successful completion of the deployment.

	![Output window reporting successful deployment](./media/web-sites-dotnet-get-started/PublishOutput.png)

	Upon successful deployment, the default browser automatically opens to the URL of the deployed web app, and the application that you created is now running in the cloud. The URL in the browser address bar shows that the web app is loaded from the Internet.

	![Web app running in Azure](./media/web-sites-dotnet-get-started/GS13deployedsite.png)

> [AZURE.TIP] You can enable the **Web One Click Publish** toolbar for quick deployment. Click **View > Toolbars**, and then select **Web One Click Publish**. You can use the toolbar to select a profile, click a button to publish, or click a button to open the **Publish Web** wizard.
> ![Web One Click Publish Toolbar](./media/web-sites-dotnet-get-started/weboneclickpublish.png)

## Monitor and manage the web app in the Azure Portal

The [Azure portal](/services/management-portal/) is a web interface that you can use to manage and monitor your Azure services, such as the web app that you just created. In this section of the tutorial, you look at some of what you can do in the portal.

1. In your browser, go to [https://portal.azure.com](https://portal.azure.com), and sign in with the credentials you use for managing your Azure account.

2. Click **App Services**, and then click the name of your web app.

	![App Services in portal](./media/web-sites-dotnet-get-started/selinportal.png)

	The **Web app** blade displays an overview of settings and usage statistics for your web app. (Windows that open to the right in the portal are called *blades*.)

	![Web app blade](./media/web-sites-dotnet-get-started/portaldashboard.png)

	At this point, your web app hasn't had much traffic and may not show anything in the graph. If you browse to your application, refresh the page a few times, and then refresh the Portal page, you'll see some statistics show up.

3. The **Settings** blade shows more options for configuring your web app.

	![Settings blade](./media/web-sites-dotnet-get-started/portalconfigure1.png)

	There area more sections to this blade than are shown in this screen shot.

4. Click **Application settings** from the **General** section of the **Settings** blade to see an example of the kinds of settings that you can configure in the Portal.

	For example, you can control the .NET version that's used for the web app, enable features such as [WebSockets](/blog/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites/), and set [connection string values](/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

	![Web app configure tab](./media/web-sites-dotnet-get-started/portalconfigure2.png)

These are just a few of the Portal's features. You can create new web apps, delete existing web apps, stop and restart web apps, and manage other kinds of Azure services, such as databases and virtual machines.  

## Next steps

In this tutorial, you've seen how to create a simple web application and deploy it to an Azure web app. Here are some related topics and resources for learning more about Azure App Service:

* Other ways to create web apps

	You saw how to create a web app while creating a Visual Studio project. You can also create Azure resources the deployment process in Visual Studio the same way you saw it done during project creation. You can also create web apps by using the [Azure portal](https://portal.azure.com/), [Azure cmdlets for Windows PowerShell](../powershell-install-configure.md), or the [cross-platform command-line interface](../xplat-cli.md).

* How to create API apps

	You've seen how to create an instance of Azure App Service that is mainly intended to host a website. App Service also has features designed to make it easier to develop, test, and host APIs. For more information, see [Get started with API Apps and ASP.NET in Azure App Service](../app-service-api/app-service-api-dotnet-get-started.md). 

* Other ways to deploy a web project

	For information about other ways to deploy web projects to web apps, by using Visual Studio or by [automating deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) from a [source control system](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), see [How to deploy an Azure web app](web-sites-deploy.md).

	Visual Studio can also generate Windows PowerShell scripts that you can use to automate deployment. For more information, see [Automate Everything (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything).

* How to troubleshoot a web app

	Visual Studio provides features that make it easy to view Azure logs as they are generated in real time. You can also run in debug mode remotely in Azure. For more information, see [Troubleshooting Azure web apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

* How to add a custom domain name and SSL

	For information about how to use SSL and your own domain (for example, www.contoso.com instead of contoso.azurewebsites.net), see the following resources:

	* [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md)
	* [Enable HTTPS for an Azure website](web-sites-configure-ssl-certificate.md)

* How to add real-time features such as chat

	If your web app will include real-time features (such as a chat service, a game, or a stock ticker), you can get the best performance by using [ASP.NET SignalR](http://www.asp.net/signalr) with the [WebSockets](/blog/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites/) transport method. For more information, see [Using SignalR with Azure web apps](http://www.asp.net/signalr/overview/signalr-20/getting-started-with-signalr-20/using-signalr-with-windows-azure-web-sites).

* How to choose between App Service, Azure Cloud Services, and Azure Virtual Machines for web applications

	In Azure, you can run web applications in App Service Web Apps as shown in this tutorial, or in Cloud Services or in Virtual Machines. For more information, see [Azure web apps, cloud services, and VMs: When to use which?](/manage/services/web-sites/choose-web-app-service/).
