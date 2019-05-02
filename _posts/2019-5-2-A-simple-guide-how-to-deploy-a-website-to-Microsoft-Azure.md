---
layout: post
title: Deploy a website to Microsoft Azure
---

Microsoft Azure is the most known cloud provider that enables you to build, deploy, monitor, and scale cloud hosted services. Deployment in Azure is flexible, you can deploy your code from Visual Studio, from GitHub, from Azure DevOps, and Azure portal. 

In this article, you'll learn how to deploy your code with this popular methods.

- Using Visual Studio Code
- Using Visual Studio 2017
- Deployment from GitHub

## 1. Using Visual Studio Code

Visual Studio Code is a popular lightweight editor which run on Windows, macOS and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has rich ecosystem for extensions for multiple languages and runtimes. VS Code doesn't include a compiler and for that the compilation for specific languages and scenarios is added via extensions.
Extensions extend the capabilities of Visual Studio Code to add a wide range of new capabilities. For example, extensions can be used to add compilers, add spell checking, and integrate with Azure services.
Extensions are free and can be added from the Extensions page within Visual Studio Code. 

### Install Azure App Service extension

To use Visual Studio Code for Azure development, you'll need to install  Azure App Service extension.

- Open VS Code in Extension tab and enter on search bar *Azure App Service* 
- Select *Azure App Service* result and click install

   ![Azure App Service](/images/SecondPost/VSExtension.png)

- Click Sign in to Azure with your account. You should see your subscription name.
- Enter `ctrl+p` to display the command palette and click Create New Web App

 ![Create Web App](/images/SecondPost/CreateWebApp.PNG)

- Enter the app name, must be unique
- Choose a location 
- Choose your framework version(Php, Node.js, .Net Version etc)

After a short amount of time a notification will shows services created for your app and your app will be displayed under your subscription. 
- Choose the directory of your project wich is open

 ![Select Folder](/images/SecondPost/SelectFolder.png)

After the deployment completes, click Browse Website in the prompt to see your deployed website.

## 2. Deploy with Visual Studio 2017

>Visual Studio 2017 is a fully featured and powerful IDE used to develop applications for a wide range of application types in including Windows, Android, iOS, web, and Azure.

When installing Visual Studio, you'll see that several workloads are available. You'll need to include: 
- **Azure development** workload which includes the Azure SDKs, tooling, and template projects
- **ASP.NET and web development** which is the development workload in Visual Studio 2017 designed to maximize your productivity in developing web applications using ASP.NET and standards-based technologies like HTML and JavaScript.

![Azure Development](/images/SecondPost/select-azure-workload.png)

Open Visual Studio and click the View menu to make sure you have the Cloud Explorer option.
At this point let's create a template ASP.NET MVC Core Project just for demostration. 

Press File and New Project.

- Select Visual C# => .NET Core => ASP.NET Core Web Application.
- Name your Solution, Project and click OK.
- Select MVC.
- On Authentication select No Authentication.

![Mvc Project](/images/SecondPost/MvcProject.PNG)

- Check the Configure for HTTPS

After a while, you will see the project in solution explorer.

![Solution Explorer](/images/SecondPost/SolutionExplorer.PNG)

Run the Application with the green button or prees F5 and you will notice the template created.

![Web Template](/images/SecondPost/Template.PNG)

Stop the application, right click on your Project and press Publish.
In the App Service tab check Create New and press Publish. Now you need to enter your app details.
- Enter your app name
- Choose your subscription
- Create a new resource group
- Create a new Hosting Plan
- Activate Application Insight, it's optional
- Finally press Create

![Create Azure Web App](/images/SecondPost/CreateAzureWebApp.PNG)

And the result in browser as you can see the app is published with the url https://my-sample.azurewebsite.net

![Azure Web App](/images/SecondPost/AzureApp.PNG)

Congratulations! You just published your first app in Azure using Visual Studio 2017. 

## 3. Deployment to Azure from GitHub

To start with, you need to create a new repository in GitHub and push an .NET Core web application that you can generate using dotnet cli tool.

###  Setup a GitHub Repository & commit a template .NET Core Web App

Let's go to github and fill in the details needed like repository name and click the **Create repository** button to get up and running with your repository. 

![Create Github Repository](/images/SecondPost/GithubRepo.png)

Now it's time for your .NET Core web app. Using dotnet commands you can create a new web app.
- use the command `dotnet new webapp -n sample-app` to create a new razor app.
- enter `cd sample-app` and `dotnet run` to run the app 

![Create with dotnet commands](/images/SecondPost/DotnetCommands.PNG)

Now you can see the app running.

![In Browser](/images/SecondPost/InBrowser.PNG)

Stop the app and to push the new dotnet web app to GitHub you need to write the following commands:

```
git remote add origin https://github.com
<your_github_account>/sample-app.git
> git push -u origin master
```

#### Connect your GitHub account with your Azure Web App

Now you need to go to the Azure portal to create your web app.

- Enter `portal.azure.com` in browser, navigate to the App Services and click Add button. Enter your app details: name, resource group, app service plan and location and click the Create button.

![Add App](/images/SecondPost/AddApp.PNG)

After your app got created scroll down, press Deployment Center and select the GitHub option.

 ![Deployment](/images/SecondPost/Deployment.PNG)

 Press the Continue button. In the next tab you need to enter your GitHub name, select your repository, branch and again press continue.

![Select repository](/images/SecondPost/SelectRepository.PNG)

Now at the end press the Finish button, wait few minutes and click the link of the web app you just created.
