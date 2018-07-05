---
title: Logging commands
description: Logging commands
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 1EA20FD4-E388-47DF-9CCF-3C2D4C27537A
ms.manager: douge
ms.author: alewis
ms.date: 04/02/2017
---

# Logging commands

[!INCLUDE [temp](../_shared/version.md)]

The general format for a logging command is:

    ##vso[area.action property1=value;property2=value;...]message

To invoke a logging command, simply emit the command via standard output. For example:

    Write-Host "##vso[task.setvariable variable=testvar;]testvalue"

![icon](../tasks/utility/_img/powershell.png) **PowerShell** (on a Windows agent)

```ps
Write-Host "##vso[task.setvariable variable=testvar;]testvalue"
```
<br/>

![icon](../tasks/utility/_img/shell-script.png) **Shell Script** (on a macOS or Linux agent)

```bash
#!/bin/bash
echo "##vso[task.setvariable variable=testvar;]testvalue"
```

## Task

### LogIssue: Log an error or warning

`##vso[task.logissue]error/warning message`

#### Usage

Log an error or warning message in the timeline record of the current task.

#### Minimum Agent Version

Any

#### Properties

* `type` = `error` or `warning` (Required)
* `sourcepath` = source file location
* `linenumber` = line number
* `columnnumber` = column number
* `code` = error or warning code

#### Example: Log an error

![icon](../tasks/utility/_img/powershell.png) **PowerShell**

```ps
Write-Host "##vso[task.logissue type=error]Something went very wrong."
exit 1
```
<br/>

![icon](../tasks/utility/_img/shell-script.png) **Shell Script**

```bash
#!/bin/bash
echo "##vso[task.logissue type=error]Something went very wrong."
exit 1
```

> [!TIP]
> 
> `exit 1` is optional, but is often a command you'll issue soon after an error is logged. If you select **Control Options: Continue on error**, then the `exit 1` will result in a partially successful build instead of a failed build.

#### Example: Log a warning about a specific place in a file

![icon](../tasks/utility/_img/powershell.png) **PowerShell**

```ps
Write-Host "##vso[task.logissue type=warning;sourcepath=consoleapp/main.cs;linenumber=1;columnnumber=1;code=100;]Found something that could be a problem."
```
<br/>

![icon](../tasks/utility/_img/shell-script.png) **Shell Script**

```bash
#!/bin/bash
echo "##vso[task.logissue type=warning;sourcepath=consoleapp/main.cs;linenumber=1;columnnumber=1;code=100;]Found something that could be a problem."
```

### SetProgress: Show percentage completed

`##vso[task.setprogress]current operation`

#### Usage

Set progress and current operation for the current task.

#### Minimum Agent Version

Any

#### Properties

* `value` = percentage of completion

#### Example

![icon](../tasks/utility/_img/powershell.png) **PowerShell**

```ps
Write-Host "Begin a lengthy process..."
$i=0
While ($i -le 100)
{
   Start-Sleep 1
   Write-Host "##vso[task.setprogress value=$i;]Sample Progress Indicator"
   $i += 10
}
Write-Host "Lengthy process is complete."
```

To see how it looks, save and queue the build, and then watch the build run. Observer that a progress indicator changes when the task runs this script.

### Complete: Finish timeline

`##vso[task.complete]current operation`

#### Usage

Finish the timeline record for the current task, set task result and current operation. When result not provided, set result to succeeded.

#### Minimum Agent Version

1.95
                
#### Properties

* `result` = 
 - `Succeeded` The task succeeded.
 - `SucceededWithIssues` The task ran into problems. The build will be completed as partially succeeded at best.
 - `Failed` The build will be completed as failed. (If the **Control Options: Continue on error** option is selected, the build will be completed as partially succeeded at best.)
 - `Cancelled` Cancels the build.
 - `Skipped` Logs the task outcome as skipped.
   
#### Example

```
##vso[task.complete result=Succeeded;]DONE
```

### LogDetail: Create and update a timeline record for a task

`##vso[task.logdetail]current operation`

#### Usage

Create and update detail timeline records.

The first time we saw `##vso[task.detail]` for each task, we will create a detail timeline for the task. We will create and update nested timeline record base on id and `parentid`.

Task author need to remember which GUID they used for each timeline record.
The logging system will keep tracking the GUID for each timeline records that been created, so any new GUID will result a new timeline record.

#### Minimum Agent Version

Any

#### Properties

* `id` = Timeline record GUID (Required)
* `parentid` = Parent timeline record GUID 
* `type` = Record type (Required for first time, can't overwrite)
* `name` = Record name (Required for first time, can't overwrite)
* `order` = order of timeline record (Required for first time, can't overwrite)
* `starttime` = `Datetime`
* `finishtime` = `Datetime`
* `progress` = percentage of completion 
* `state` = `Unknown` | `Initialized` | `InProgress` | `Completed` 
* `result` = `Succeeded` | `SucceededWithIssues` | `Failed` | `Cancelled` | `Skipped`

#### Examples

Create new root timeline record: 

```
##vso[task.logdetail id=new guid;name=project1;type=build;order=1]create new timeline record
```

Create new nested timeline record: 

```
##vso[task.logdetail id=new guid;parentid=exist timeline record guid;name=project1;type=build;order=1]create new nested timeline record
```

Update exist timeline record: 

```
##vso[task.logdetail id=exist timeline record guid;progress=15;state=InProgress;]update timeline record
```

### SetVariable: Initialize or modify the value of a variable

`##vso[task.setvariable]value`

#### Usage

Sets a variable in the variable service of taskcontext. The first task can set a variable, and following tasks are able to use the variable. The variable is exposed to the following tasks as an environment variable.

When `issecret` is set to `true`, the value of the variable will be saved as secret and masked out from log. Secret variables are not passed into tasks as environment variables and must instead be passed as inputs.

#### Minimum Agent Version

Any

#### Properties

* `variable` = variable name (Required)
* `issecret` = `true` (Optional)
   
#### Examples

![icon](../tasks/utility/_img/powershell.png) **PowerShell** Set the variables.

```ps
Write-Host "##vso[task.setvariable variable=sauce;]crushed tomatoes"
Write-Host "##vso[task.setvariable variable=secretSauce;issecret=true]crushed tomatoes with garlic"
```
<br/>

![icon](../tasks/utility/_img/powershell.png) **PowerShell** Read the variables.

```ps
Param(
   [string]$sauceArgument,
   [string]$secretSauceArgument
)
Write-Host No problem reading $env:sauce or $sauceArgument
Write-Host But cannot read $env:secretSauce
Write-Host But I can read $secretSauceArgument "(but log is redacted so I can't expose the value)"
```

Console output:

```
No problem reading crushed tomatoes or crushed tomatoes
But cannot read 
But I can read ******** (but log is redacted to keep it secret)
```

### AddAttachment: Attach a file to the build

`##vso[task.addattachment]value`

#### Usage

Upload and attach attachment to current timeline record. These files are not available for download with logs. These can only be referred to by extensions using the type or name values.

#### Minimum Agent Version

Any

#### Properties

* `type` = attachment type (Required)
* `name` = attachment name (Required)
  
#### Example

```
##vso[task.addattachment type=myattachmenttype;name=myattachmentname;]c:\myattachment.txt
```

### UploadSummary: Add some Markdown content to the build summary

`##vso[task.uploadsummary]local file path`

#### Usage

Upload and attach summary markdown to current timeline record. This summary shall be added to the build/release summary and not available for download with logs.

#### Minimum Agent Version

0.5.6

#### Examples

```
##vso[task.uploadsummary]c:\testsummary.md
```

It is a short hand form for the command

```
##vso[task.addattachment type=Distributedtask.Core.Summary;name=testsummaryname;]c:\testsummary.md
```

### UploadFile: Upload a file that can be downloaded with task logs

`##vso[task.uploadfile]local file path`

#### Usage

Upload user interested file as additional log information to the current timeline record. The file shall be available for download along with task logs.

#### Minimum Agent Version

1.101

#### Example

```
##vso[task.uploadfile]c:\additionalfile.log
```

## Artifact

### Associate: Initialize an artifact

`##vso[artifact.associate]artifact location`
                
#### Usage

Create an artifact link. Artifact location must be a file container path, VC path or UNC share path.

#### Minimum Agent Version

Any

#### Properties

* `artifactname` = artifact name (Required)
*  `type` = `container` | `filepath` | `versioncontrol` | `gitref` | `tfvclabel`, artifact type (Required)

#### Examples

```
##vso[artifact.associate type=container;artifactname=MyServerDrop]#/1/build
```

```
##vso[artifact.associate type=filepath;artifactname=MyFileShareDrop]\\MyShare\MyDropLocation
```

```
##vso[artifact.associate type=versioncontrol;artifactname=MyTfvcPath]$/MyTeamProj/MyFolder
```

```
##vso[artifact.associate type=gitref;artifactname=MyTag]refs/tags/MyGitTag
```

```
##vso[artifact.associate type=tfvclabel;artifactname=MyTag]MyTfvcLabel
```

### Upload: Upload an artifact

`##vso[artifact.upload]local file path`

#### Usage

Upload a local file into a file container folder, and optionally publish an artifact as `artifactname`.

#### Minimum Agent Version

Any

#### Properties

* `containerfolder` = folder that the file will upload to, folder will be created if needed. (Required)
* `artifactname` = artifact name

#### Example

```
##vso[artifact.upload containerfolder=testresult;artifactname=uploadedresult;]c:\testresult.trx
```

## Build

### UploadLog: Upload a log

`##vso[build.uploadlog]local file path`

#### Usage

Upload user interested log to build's container "`logs\tool`" folder.

#### Minimum Agent Version

Any

#### Example

```
##vso[build.uploadlog]c:\msbuild.log
```
        
### UpdateBuildNumber: Override the automatically generated build number

`##vso[build.updatebuildnumber]build number`

#### Usage

You can automatically generate a build number from tokens you specify in the [definition options](../define/options.md). However, if you want to use your own logic to set the build number, then you can use this logging command.

#### Minimum Agent Version

1.88

#### Example

```
##vso[build.updatebuildnumber]my-new-build-number
```

### AddBuildTag: Add a tag to the build

`##vso[build.addbuildtag]build tag`


#### Usage

Add a tag for current build.

#### Minimum Agent Version

1.95

#### Example

```
##vso[build.addbuildtag]Tag_UnitTestPassed
```

## Task reference

Use these tasks to run scripts:

* ![icon](../tasks/utility/_img/powershell.png) [Utility: PowerShell](../tasks/utility/powershell.md) Run a PowerShell script.

* ![icon](../tasks/utility/_img/shell-script.png) [Utility: Shell script](../tasks/utility/Shell-script.md) Run a shell script using bash.