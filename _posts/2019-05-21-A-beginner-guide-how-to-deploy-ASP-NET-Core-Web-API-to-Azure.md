---
layout: post
title: A beginner guide how to deploy ASP .NET Core Web API to Azure
---

In this article I will show you how to deploy a ASP .NET Core Web API to Azure. Even if this a beginner guide you need to have some basic knowledge of Azure Web Apps, Visual Studio Code and ASP .NET Core Web API. 

## What you need for development enviroment

Tools you need to get started are:
- Visual Studio Code [Download VS Code](https://code.visualstudio.com/Download)
- Free Microsoft Azure account [Azure Free Account](https://azure.microsoft.com/en-us/free/)
- .NET Core 2.2
- Postman [Download Postman](https://www.getpostman.com/downloads/)

Well let's get started!

## 1. Create ASP .NET Core Web API

To create a template ASP .NET Core Web API I'll use .NET Core CLI and VS Code to inspect the code but you can use Visual Studio 2017 or 2019. The result will be the same.

Open command prompt, I use `git bash` and enter the command:
```
dotnet new webapi --name AzAPI
```

![Create ASP .NET Core Web API](/images/Fourth_Post/1.PNG)

and a project with just the basic for a API it is created in my desktop.
Then enter the `cd AzPI` command to get inside the project folder and execute the Web API with the `donet run` command. 

![Execute the Web API](/images/Fourth_Post/2.PNG)

In command prompt you will see the message `Now listening on: https://localhost:5001` copy the link and `/api/values` at the end of the link. Now you can check the browser your API executed.

![Displaying in browser](/images/Fourth_Post/3.PNG)

## Using Visual Studio Code to work with the code

First stop the project running with `Ctrl+C` and enter the command `code .` to open the project in VS Code. 

![In VS Code](/images/Fourth_Post/4.PNG)

As you see in Explorer on VS Code the project has different files and folder. 

**Startup.cs** -- .NET Core use this class to configure services needed by the application and to define the request handling pipeline. The class include two methods:

- **ConfigureServices** -- wich is used for service configuration to the container and consumed across the app via DI (dependency injection). It is optional and called by the web server before the Configure method.
- **Configure** -- the method it is required and create the app's request processing pipeline.

**Program.cs** -- It is the starting point of the app and used to create a web server.

## Working with Postman

Because we are working with RESTful API we need to test our rest methods in Postman.

>Postman is a powerful HTTP client for testing web services.

Postman makes it easy to test, develop and document APIs by allowing users to quickly put together both simple and complex HTTP requests. Postman is available as both a Google Chrome Packaged App and a Google Chrome in-browser app. 

To test the pre-existing API Controller `ValuesController` which route is `api/values` first we need to execute the app with `dotnet run` and second enter the full url `http://localhost:5000/api/values in Postman.

![Postman](/images/Fourth_Post/5.PNG)

In the photo above I have tested the method GET but you can use Postman to test others methods that your app contains.

## Deploy the .Web API to Azure

To deploy the web application to Azure, we need an Azure account. If you don’t have one, you may create a free account in Azure at first.
Once we have the Azure account ready, we need to create a new using VS Code.
Before start creating the web app in Azure we need to install the Azure App Service extension in VS Code.
Enter `Azure App Service` on VS Code search bar.

![Azure App Service extension](/images/Fourth_Post/6.PNG)

Well now let's start deploying our web app. There are two ways for you to create the web app.
1. Click the Azure App Service extension. Log into your Azure account - in the Activity Bar, click on the Azure logo to show the AZURE APP SERVICE explorer. Click Sign in to Azure... and follow the instructions. 
2. Enter `Ctrl+Shift+p` to display the command palette in VS Code and select `Create new web app` 

![Create web app](/images/Fourth_Post/7.PNG)

After the is created you'll prompted to `Deploy to web app?`. 

![Deploy to azure](/images/Fourth_Post/8.PNG)

Press Yes and then in command palette you need to select the path of the folder where your project is.

![Select the folder to deploy](/images/Fourth_Post/9.PNG)

After few seconds you'll see a prompt in right-down corner with the message `Deployment to az-api completed`.

![Deployment complete](/images/Fourth_Post/10.PNG)

Click Browse WebSite and enter `api/values` at the end of url and finaly you'll see the app diplaying on the browser the same json message as above.

![Display in Browser](/images/Fourth_Post/11.PNG)
