---
layout: post
title: How to deploy Azure resources using Terraform
---

How to create azure resources by using Terraform Azure Provider? I found the experience simple and easy-going mostly because of my previews experience with Azure ARM Templates which are more complicated and hard to maintain.

In this article I will show how to deploy an Azure SQL database using the advantages of Terraform. First we need to have the necessary tools:

1. Azure subscription 
2. Terraform installed 
3. Visual Studio Code 
4. Azure CLI for authentication

Let's create a folder in preferred location and with the right of mouse open in VS Code. I have created five file:

- main.tf for the azure resources
- varibles.tf to store the recourse names and other variables needed
- outputs.tf to display the recourse outputs during the deployment
- storeState.tf to persisting of state in remote azure storage account
- secrets.tf to store the password in azure keyvault

The code in main.tf file are the two azure resources needed to deploy an azure MSSQL database.

```json

resource "azurerm_sql_server" "sql" {
  name                         = var.sql_server_name
  resource_group_name          = data.azurerm_resource_group.sql.name
  location                     = var.location
  version                      = var.sv_version
  administrator_login          = var.admin_login
  administrator_login_password = data.azurerm_key_vault_secret.secret.value

  tags = {
    server            = "Azure"
  }

}


resource "azurerm_sql_database" "sql" {
  name                             = var.db_name
  resource_group_name              = data.azurerm_resource_group.sql.name
  location                         = var.location
  server_name                      = azurerm_sql_server.sql.name
  edition                          = var.db_edition
  collation                        = var.db_collation
  create_mode                      = "Default"
  requested_service_objective_name = "Basic"

  tags = {
    db            = "Azure Database
  }

}

resource "azurerm_sql_firewall_rule" "sql" {
  name                = var.sv_firewall
  resource_group_name = data.azurerm_resource_group.sql.name
  server_name         = azurerm_sql_server.sql.name
  start_ip_address    = "0.0.0.0"
  end_ip_address      = "0.0.0.0"
}

```

All the values which starts with data. like

` data.azurerm_resource_group.sql.name `

are referencing in existing resources and in this case is deploying the resources in an existing resource group.

All the values which starts with var like

` var.db_name `

are referencing in variables stored in variables.tf

```json

variable "location" {
default = "East US"
}

variable "rg_name" {
  default = "NetworkWatcherRG"
}

variable "sql_server_name" {
  default = "sv-name"
}

variable "sv_version" {
  default = "12.0"
}

variable "admin_login" {
  default = "sv-user"
}

variable "db_name" {
  default = "db-name"
}


variable "db_edition" {
  default = "Basic"
}

variable "db_collation" {
  default = "SQL_Latin1_General_CP1_CI_AS"
}

variable "sv_firewall" {
  default = "allow-azure-services"
}
```

In storeStates.tf file as I mention above we will store Terraform state back end configurations.

```json
terraform {
backend "azurerm" {
resource_group_name = "<resource group name>"
storage_account_name = "<storage account name>"
container_name = "<container name>"
key = "terraform.tfstate"
}
}
```

We must define an existing storage account and the container.

> Terraform state is used to reconcile deployed resources with Terraform configurations. State allows Terraform to know what Azure resources to add, update, or delete.

In secrets.tf file we will store the admin password.

```json

data "azurerm_key_vault" "keyvault" {
    name = "<keyvault name>"
    resource_group_name = "rg name"
}

data "azurerm_key_vault_secret" "secret" {
name = "password" # name of keyvault secret where you have stored the password
key_vault_id = data.azurerm_key_vault.keyvault.id
}

```

We can retrieve the admin password by using:

` administrator_login_password = data.azurerm_key_vault_secret.secret.value `

At last we write in ouputs.tf the code:

```json
output "sql_server_fqdn" {
  value = "${azurerm_sql_server.sql.fully_qualified_domain_name}"
}


output "database_name" {
  value = "${azurerm_sql_database.sql.name}"
}

```

This output will displayed after the deployment success.

Now we are ready to deploy the resources on azure by using the commands

- az login to login in your azure subscription
- terraform init to start the initialization of terraform
- terraform plan to create an execution plan, but doesn't execute it.
- terraform apply to apply the execution plan.

That's it. And after everything goes well the resources will be showed in Azure portal.

Almost finished! If you want to delete the resources you have created you can use the command:

` terraform destroy `
