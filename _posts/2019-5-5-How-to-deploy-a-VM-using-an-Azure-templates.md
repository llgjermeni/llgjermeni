---
layout: post
title: How to deploy a VM using an Azure templates
---

In this particle, I’ll show you a basic guide of how to deploy Virtual Machine using an Azure template. Template can be used to deploy one/multiple Virtual Machines and of course other services.
But first let's understand the role of Azure Resource Manager.

Azure Resource Manager (ARM) with its infrastructure management platform can provide a resource group capability. So you could use and create resources that you need and bundle them up logically into a container which is called a resource group. The other thing it offers you is the object of this article is what we call deployment templates.
The entire set up of creating a resource group with all the resources in it can be scripted in a template with just JSON.

The Azure classic, the management portal was on XML, but the new (ARM) is very lightweight, and runs off the open source JSON notification format. At the center of everything is the workload that Azure offers.
For example, within Microsoft.Compute, you can have different resource types. You could have availability sets, you could have virtual machines and so on and so forth.

### What's Azure Resource Manager?

>As the name suggests, Azure Resource Manager is a service that allows you to manage all the resources that you create in an Azure subscription. 
With Azure Resource Manager, all resources are created within a resource group, which is a logical entity that is used to group resources in Azure. 

For example, when you create a VM, it comprises a resources group that contains everything, such as storage, compute, network card, public IP address, and network security groups (NSGs), all of which can be controlled independently.

Resource Manager provides a consistent management layer for the tasks that you perform through Azure PowerShell, Azure CLI, Azure portal, REST API, and development tools. 

#### Benefits of using Azure Resource Manager 

- Deploy, manage, and monitor all the resources as a group.
- Deploy multiples times the same solution.
- Can manage your resources through templates rather than scripts.
- Define the dependencies between resources to ensure they are in the correct order.
- Having access control to all services in your resource group using Role-Based Access Control (RBAC).
- Using tags to organize all resources in your subscription.
- Viewing billing by costs for a group of resources that share the same tag.

### Azure Resource Manager Template Structure

An ARM template is just JSON file that defines the resources you need to deploy for your solution. The size of the template must be up to 1 megabyte (MB), and each parameter file up to 64 kilobytes (KB). 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "",
  "apiProfile": "",
  "parameters": {  },
  "variables": {  },
  "functions": [  ],
  "resources": [  ],
  "outputs": {  }
}
```

- `$Schema`: Location of the JSON schema file 
- `contentVersion`: Version of the template (such as 1.0.0.0).
- `parameters`: Optional values that are provided when deployment is executed to customize resource deployment.
- `variable`: Values that are used as JSON fragments in the template to simplify template language expressions. 
- `functions`: User-defined functions that are available within the template.
- `resources`: A manageable item that is available through Azure. Some common resources are a virtual machine, storage account, web app, database, and virtual network, but there are many more.
- `outputs`: Values that are returned after deployment

The allowed types for values are:
- `string` or `secureString` – a valid JSON string
- `int` – a valid JSON integer
- `bool` – a valid JSON boolean
- `object` – a valid JSON object
- `array` – a valid JSON array

### Create a VM using Visual Studio 2017

Let’s start creating a Azure VM using Visual Studio and ARM templates. To create a template with Visual Studio, you can use many different starter templates for creating and deploying multiple Azure resources. In this section, you'll create and deploy a simple VM. 
So, let’s create a new project with File -> New Project and select Azure Resource Group located under the Cloud item.

![Create template](/images/ThirdPost/1.png)

Click OK and a wizard will show up where you need to choose the type of resource we are trying to deploy. We can start from scratch by selecting Blank Template or pick any of the templates available wich is our case, so we select Windows Virtual Machine provided by Microsoft. I need to note here that we can use this window again to add a resource later on through the graphical user interface.

![Select VM](/images/ThirdPost/2.png)

Your template is now created in Visual Studio where you can see the json file and powershell file. Basically, on the right side Solution Explorer you can see all files that are part of the current solution `azuredeploy.json` and `azuredeploy.parameters.json` files. If you double click on one of the files, that will be open in editor, and you can edit the code by clicking on any element which is displayed in JSON Outline tab.

![Files in VS](/images/ThirdPost/3.png)

Every JSON file contains four main sections: 

- parameters
- variables
- resources
- output 

Where we will add our code to deploy our Azure resources. In the left side JSON Outline, you have a listed items, for any new entry in the code, an icon will be displayed in the left side which helps to understand the items that are being added and for navigation purposes.

Right-click your project name in Visual studio and choose Deploy -> New Deployment.

![Deploy](/images/ThirdPost/4.png)

Choose your Azure subscription
Select an existing or create a new resource group. And finally click Deploy.

![add values](/images/ThirdPost/5.png)

You'll get prompted for parameters values.
Enter the information and click save.

In few minutes, you'll get a ready to use Virtual Machine on Azure!

Congratulation! You now have created a Azure VM. 
