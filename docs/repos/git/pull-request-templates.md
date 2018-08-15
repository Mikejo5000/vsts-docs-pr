---
title: Improve your pull request descriptions with pull request templates | VSTS & TFS
description:  Learn how to improve pull request descriptions using pull request templates
ms.assetid: 4C9DFD24-E894-454A-A080-DA511C90CA74
ms.prod: devops
ms.technology: devops-code-git 
ms.manager: douge
ms.author: sdanie
author: steved0x
ms.topic: conceptual
ms.date: 04/03/2018
monikerRange: 'vsts'
---

# Improve your pull request descriptions with pull request templates

#### VSTS 

A good pull request description can help reviewers be effective when reviewing pull requests. Pull request templates can help your pull request creators to create good pull request descriptions that meet your organization's standards.

This article shows you how to get started with pull request templates.

## What is a pull request template?

A pull request template is a block of text or markdown that can be added to your pull request description when the pull request is created. VSTS allows you to create the following type of pull request templates:

- Default - these pull request templates are automatically applied to pull request descriptions for all pull requests in the repo, unless a branch specific pull request template applies
- Branch specific - these pull request templates are automatically applied to pull requests targeting a specific branch
- Optional - these pull request templates can be optionally added by the pull request creator

A pull request template is a markdown file or text file located in a designated folder. When the pull request template is applied, the contents of the pull request template are placed in the pull request description. If the following snippet was the default pull request template for a repo, it would automatically be set as the description for any pull request into that repo (unless there was a more specific branch pull request template).

```
Thank you for your contribution to the Fabrikam Fiber repo. Before submitting this PR, please make sure:

[] Your code builds clean without any errors or warnings
[] You are using approved terminology
[] If your PR covers more than 25 files, please break it up into smaller PRs if possible
```

## Pull request template locations


Default template that applies to every PR targeting the repo:

Must be named pull_request_template.md or .txt

File location for default pull request template. Must be in 1 of 3 places:
Root folder, .vsts folder, or docs folder

Does it automatically append to the description? Or do you have to click it for a default template? Ok it automatically appears.



Other non-default templates can be specified by choosing them from a drop down under the PR description box. They can also be specified by adding ?template=name.md (or txt) to the URL. Must specify extension if the file has one? Allowed to not?

Must be in a folder named pull_request_template and this folder must be in the root folder, .vsts folder, or docs folder

Branch specific templates will override the template if a user targets a specific branch

Naming:
Must match first level of branch name (i.e. master, dev, releases, feature, etc.)
Can have an extension such as .md or .txt 
Master.md would be displayed any time a PR targets master branch or any master/* branches.
Releases.txt would be used any time a PR targets releases/* branches.
Must be in the folder:
PULL_REQUEST_TEMPLATE/branches
"branches" must be lower case
Like multiple templates, can be in the root or a subfolder of .vsts or docs




