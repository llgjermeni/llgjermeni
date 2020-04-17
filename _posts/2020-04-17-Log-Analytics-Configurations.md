---
layout: post
title: Log Analytics Configurations
---

>Azure Monitor maximizes the availability and performance of your applications and services by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments. It helps you understand how your applications are performing and proactively identifies issues affecting them and the resources they depend on.

Let set what we can do with Azure Monitor:

1. Detect and diagnose issues across applications using Application Insights.
2. You can use Azure Monitor to detect issues for VMs and Containers.
3. Use the Log Analytics for troubleshooting and deep diagnostics.
4. Support operations at scale with smart alerts and automated actions.
5. Create visualizations with Azure dashboards and workbooks.

In this tutorial I will show you how to configure Log Analytics to monitor resources like Azure VM, local pc, Azure Storage, Azure VM Scalability Set, Azure AKS, Azure Event Hub and Azure Cosmos DB.
## How to create Log Analytics

Let’s start. First, we need to create Azure Log Analytics. In All resources click Add and on search bar enter Log Analytics. 

![Create Azure Log Analytics](/images/log_analytics_configuration/1.PNG)


Enter the Workspace name, resource group, location and click OK.
After you created the Log Analytics now you need to create two Azure VM, one Linux Vm and one Windows VM. You can create these VMs using azure portal or PowerShell.

Supposing you know how to create azure Virtual machine or already have these on your subscription.

![Create Azure Log Analytics](/images/log_analytics_configuration/2.PNG)

Now we need to connect these VM's with the Log Analytics. Go to your Log Analytics that you just created and under Workspace Data Sources click Virtual Machine.

![Create Azure Log Analytics](/images/log_analytics_configuration/3.PNG)

As you see in image all VM’s and VMSS’s click the desired VM, we need to connect the linux-vm and the win-vm. Click the name of desired VM and click Connect. Do the same for all VM’s or VMSS’s to connect them with the selected Log Analytics.

![Create Azure Log Analytics](/images/log_analytics_configuration/4.PNG)

After you connected all VM’s and VMSS’s(Virtual Machine Scale Set) you will see an image like the below.

![Create Azure Log Analytics](/images/log_analytics_configuration/5.PNG)


### Configure the VM to use the Log Analytics

Now we need to make the configuration from the VM. So, let’s go to the VM, I have chosen the linux-vm. Go to linux-vm and under Monitoring click Insights and after that click Enable.

![Create Azure Log Analytics](/images/log_analytics_configuration/6.PNG)

After few minutes you will see the logs of the VM. Click the Performance button and you will see the performance logs detailed in charts.

![Create Azure Log Analytics](/images/log_analytics_configuration/7.PNG)

You can click also the Azure Monitor to see more details from the logs.

![Create Azure Log Analytics](/images/log_analytics_configuration/8.PNG)

But let’s go to the Log Analytics page to see other details about the VM’s. On the Log Analytics click Advanced settings.

![Create Azure Log Analytics](/images/log_analytics_configuration/9.PNG)

On Windows Servers you will see two computers connected one is the Azure VM and the other is my PC. 

To connect a local computer, you need to download the Windows Agent that you see on the image. Is the same as you install a normal software, but you need to add the Workspace ID and the Primary Key when is asked. Now click on 2 Windows Computers Connected to see the Windows VM logs.

![Create Azure Log Analytics](/images/log_analytics_configuration/10.PNG)

As you see on image click Chart and select the Computer. So, with win-name is the azure vm I have created and with Laert name is my PC.

For the Linux VM’s you can do the same steeps you have done with the windows computer. Let’s click Linux Servers and select the 2 Linux Computers Connected.
![Create Azure Log Analytics](/images/log_analytics_configuration/11.PNG)

The 2 Computers connected are one the Azure Linux VM with name linux-vm that I have created before and the other is the Linux VMSS’s that I already have on my subscription.

![Create Azure Log Analytics](/images/log_analytics_configuration/12.PNG)

### Connect Azure Storage with Azure Log Analytics

You can connect the Azure Storage with Azure Log Analytics to collect logs. Diagnostic settings will collect resource logs for Azure compute resources like any other resource, but not their guest operating system or workloads.

![Create Azure Log Analytics](/images/log_analytics_configuration/13.PNG)

If you want to add other Storage click Add, select the storage account you want to collect the logs and select the Data Type of logs you want to collect.

![Create Azure Log Analytics](/images/log_analytics_configuration/14.PNG)

### Connect Azure Event Hub with Azure Log Analytics
To connect Azure Event Hubs with Azure Log Analytics you need to create first Event Hub Namespace and Event Hub using an existing one. After you created the Event Hub under the Monitoring click Diagnostics settings.

![Create Azure Log Analytics](/images/log_analytics_configuration/15.PNG)

Click Add diagnostics settings and just for demonstration purpose I have checked all the check box. I have selected the logs and metrics, the Log Analytics Workspace as destination, the Storage account to collect the logs and also, I have selected the Event Hub for streaming.

![Create Azure Log Analytics](/images/log_analytics_configuration/16.PNG)

Click save and you have connected the Event Hub with Azure Log Analytics.

![Create Azure Log Analytics](/images/log_analytics_configuration/17.PNG)

Now click on Logs to see the logs details from the Event Hub. There is not match logs because this is a test Event Hub.

![Create Azure Log Analytics](/images/log_analytics_configuration/21.PNG)

### Connect Azure Cosmos DB with Azure Log Analytics

To connect Cosmos Db with Log Analytics you need to create first a Cosmos DB or you already have one. After you created the Cosmos DB go under the Monitoring click Diagnostics settings. Click Add diagnostics settings where I have selected the logs and metrics, the Log Analytics Workspace as destination, the Storage account to collect the logs and also, I have selected the Event Hub for streaming.

![Create Azure Log Analytics](/images/log_analytics_configuration/18.PNG)

Click save and you have connected the Cosmos DB with Azure Log Analytics.

![Create Azure Log Analytics](/images/log_analytics_configuration/19.PNG)

Now click on Logs to see the logs details from the Cosmos DB. There is not match logs because this is a test Cosmos DB.

![Create Azure Log Analytics](/images/log_analytics_configuration/20.PNG)

### Connect Azure Kubernetes Services with Azure Log Analytics

To connect the AKS with Azure Log Analytics you need to create it first. Under the Monitoring select Insight. On Log Analytics workspace select the desired Log Analytics Workspace and click the Enable button.

![Create Azure Log Analytics](/images/log_analytics_configuration/22.PNG)

After the Log Analytics is enabled click the Logs button and see the logs.

![Create Azure Log Analytics](/images/log_analytics_configuration/23.PNG)

To see more details, you need to have some kind of activity from the AKS.  






