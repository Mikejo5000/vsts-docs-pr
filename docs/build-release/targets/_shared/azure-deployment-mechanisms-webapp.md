All of the examples above rely on built-in [Azure App Service Deploy task](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/AzureRmWebAppDeployment) in VSTS that provides simplified integration with Azure. If you use a Windows VSTS agent, this task relies on Web Deploy technology to interact with the Azure web app. Web Deploy provides several convenient deployment options such as renaming locked files, excluding files from App_Data folder during dpeloyment, etc. You can use these options when using the task in your YAML file. 

If you use an agent on Linux platform, then the task relies on [Kudu REST APIs](https://github.com/projectkudu/kudu/wiki/REST-API).

The [Azure App Service Manage task](https://docs.microsoft.com/vsts/build-release/tasks/deploy/azureappservicemanage.0?view=vsts) is another task that you can use to start, stop, or restart the web app prior to or after deployment. This task can also be used to swap slots, install site extensions, or enable monitoring of the web app.

If the built-in tasks do not meet your needs, then you can use one of the following ways to script your deployment. View the YAML snippets in each of these tasks for examples of how to use them.

* [Azure Powershell task](https://docs.microsoft.com/vsts/build-release/tasks/deploy/azurepowershellv3.3?view=vsts)
* [Azure CLI task](https://docs.microsoft.com/vsts/build-release/tasks/deploy/azure-cli?view=vsts)
* [FTP task](https://docs.microsoft.com/vsts/build-release/tasks/utility/ftp-upload?view=vsts)
