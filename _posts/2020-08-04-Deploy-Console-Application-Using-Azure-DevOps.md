---
layout: post
title: Deploy Console Application Using Azure DevOps
---

This is a tutorial where I will show you step by step how to deploy a Console App on Azure Virtual Machine using Azure DevOps.

First you need to have a console application which run successfully in local. After that you need to create a project on azure devops. In this project you can upload the console app using git from you PC or from GitHub. 
If you are using github then start by creating the build pipeline. 

![Pull the console app code from GitHub](/images/DeployConsoleApp/1.png)

Select the repository you have the project and after that select .Net Desktop.

![Configure the Pipeline](/images/DeployConsoleApp/2.png)

You will see the azure-pipelines.yml and add the following code on this file.

```yaml
# .NET Desktop
# Build and run tests for .NET Desktop or Windows classic desktop solutions.
# Add steps that publish symbols, save build artifacts, and more:
# https://docs.microsoft.com/azure/devops/pipelines/apps/windows/dot-net

trigger:
- master

pool:
  vmImage: 'windows-latest'

variables:
  solution: '**/*.sln'
  buildPlatform: 'Any CPU'
  buildConfiguration: 'Release'

steps:
- task: NuGetToolInstaller@1

- task: NuGetCommand@2
  inputs:
    restoreSolution: '$(solution)'

- task: VSBuild@1
  inputs:
    solution: '$(solution)'
    msbuildArgs: '/p:OutputPath="$(Build.BinariesDirectory)\$(Build.BuildId)"'
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: ArchiveFiles@2
  inputs:
    rootFolderOrFile: '$(Build.BinariesDirectory)\$(Build.BuildId)'
    includeRootFolder: false
    archiveType: 'zip'
    archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip'
    replaceExistingArchive: true

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'drop'
    publishLocation: 'Container'
```

Now you can save and run the build pipeline. With this code the pipeline will run successfully.

In next step you will create the release pipeline. First you create a Deployment Group on azure devops.

![Deployment Group](/images/DeployConsoleApp/3.png)

You can check the checkbox `Use personal access token in the script for authentication` and after that click the button `Copy script to the clipboard`.

Go to your azure virtual machine and open the powershell as administrator and paste the powershell script on it. Click enter and wait until the script will run and the azure vm will be connected with the azure devops using this script agent.

Create the release pipeline and click on the three dots and select Add a deployment group job. After that click the plus `+` sign and add 4 tasks like in the image below. 
![Build Pipeline](/images/DeployConsoleApp/4.png)

1. The first task will be the Unistall is a cmd task.

![Unistall cmd task](/images/DeployConsoleApp/5.png)

Enter the name and on script box enter the script you see. Just you need to change the name of your project. My project name is DeployConsole, change it with you app name. 

2. Click on `+` sign and add Extract files task and make the changes as in the image bellow.

![Extract files](/images/DeployConsoleApp/6.png)

Click on the `+` sign and add the File Transform and make the changes as in the image bellow.

![File Transform](/images/DeployConsoleApp/7.png)

Click on the `+` sign and add the cmd task and make the changes as in the image bellow.

![Install cmd task](/images/DeployConsoleApp/8.png)

At the end you can add the artifact and select your project and your build pipeline. 
Now you can run and deploy the release pipeline.