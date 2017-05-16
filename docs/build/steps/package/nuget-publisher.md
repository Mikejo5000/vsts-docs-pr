---
title: NuGet Publisher
description: How to publish NuGet packages when building code in Visual Studio Team Services
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: E592A505-C253-4190-86D2-E4F679F5FCBE
ms.manager: douge
ms.author: alewis
ms.date: 08/10/2016
---

# Package: NuGet Publisher

[!INCLUDE [temp](../../_shared/version-tfs-2015-update.md)]

![](_img/nuget-publisher.png) Publish your NuGet package to a server and update your feed.

> [!TIP]
> Looking for help to get started? See [Use Team Build to restore and publish NuGet packages](../../../package/build/team-build-nuget.md).

## Demands

None

## Arguments

<table>
<thead>
<tr>
<th>Argument</th>
<th>Description</th>
</tr>
</thead>
<tr>
<td>Path/Pattern to nupkg</td>
<td>
<p>Specify the packages you want to publish.</p>
<ul>
<li>Default value: ```**\*.nupkg;-:**\packages\**\*.nupkg```</li>
<li>To publish a single package, click the <strong>...</strong> button and select the file.</li>
<li>Use single-folder wildcards (```*```) and recursive wildcards (```**```) to publish multiple packages.</li>
<li>Use [variables](../../define/variables.md) to specify directories. For example, if you specified ```$(Build.StagingDirectory)\packages``` as the **package folder** in the [NuGet Packager](nuget-packager.md) step, you could specify ```$(Build.StagingDirectory)\packages\**\*.nupkg``` here.</li>
</ul>
<!-- https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/NugetPublisher/task.json says you can specify multiple patterns separated by semicolons. That doesn't seem to work -->
</td>
</tr>
<tr>
<td>Feed type</td>
<td>
<ul>
<li>**External NuGetFeed** publishes to an external server such as [NuGet](https://www.nuget.org/) or [MyGet](http://www.myget.org/). After you select this option, you create and select a **NuGet server endpoint**.
</li>
<li>**Internal NuGet Feed** publishes to an internal or  Visual Studio Team Services feed. After you select this option, you specify the **internal feed URL**.
</li>
</ul>
</td>
</tr>
<tr><th style="text-align: center" colspan="2">Advanced</th></tr>
<tr>
<td>NuGet Arguments</td>
<td>
(Optional) Additional arguments passed to [nuget push](https://docs.nuget.org/consume/command-line-reference#user-content-push-command).
</td>
</tr>
[!INCLUDE [temp](../_shared/nuget-step-arguments.md)]
[!INCLUDE [temp](../_shared/control-options-arguments.md)]
</table>


## Examples

[!INCLUDE [temp](../_shared/nuget-create-step-examples.md)]

## Related steps

![](_img/nuget-packager.png) [NuGet Packager](nuget-packager.md) Create a NuGet package from either a .csproj or .nuspec file

![](_img/nuget-installer.png) [NuGet Installer](nuget-installer.md) Install and update NuGet package dependencies


## Q & A

<!-- BEGINSECTION class="md-qanda" -->

[!INCLUDE [temp](../_shared/nuget-step-qa.md)]

### What happens if no packages are found to publish? Does the task succeed?

Yes

### Can I delete a package?

Depends on the server:

* Your own NuGet server: Yes. See [Delete Command](https://docs.nuget.org/consume/command-line-reference#user-content-delete-command)

* Visual Studio Team Services: No. And you can't delist one yet.

* NuGet.org: No, but you can unlist packages. See https://docs.nuget.org/Create/Deleting-Packages 

[!INCLUDE [temp](../../_shared/qa-agents.md)]

[!INCLUDE [temp](../../_shared/qa-versions.md)]

<!-- ENDSECTION -->