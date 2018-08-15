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
Thank you for your contribution to the Fabrikam Fiber repo. 
Before submitting this PR, please make sure:

[] Your code builds clean without any errors or warnings
[] You are using approved terminology
[] If your PR covers more than 25 files, please break it up into smaller PRs
```

## Default pull request templates

Default pull request templates are automatically applied to the description field when a new PR is created. To configure your repository with a default pull request template, create a file named pull_request_template.md or pull_request_template.txt and save it in your repo in one of the following folders.

- The root folder of the repo
- A folder named `.vsts` that is contained in the root folder of the repo
- A folder name `docs` that is contained in the root folder of the repo

>[!NOTE]
>Multiple locations are provided to give you flexibility in where you store your pull request templates in your repo. When a pull request is created VSTS searches the previous folders in the order given, and uses the first default pull request template it finds.

When a new pull request is created in the repo, unless a more specific branch pull request template applies, the contents of the default pull request template are used for the description field in the pull request. You can edit or add to this description and append additional pull request templates if desired.

## Branch specific pull request templates

Branch specific pull request templates can be configured for pull requests that target a specific branch. To configure your repository with a branch specific pull request template, create a pull request template (`*.md` or `*.txt`) named after your branch. The name must match the first level of the branch name, such as `master`, `dev`, `release`, `feature`.Each branch specific pull request template is applied any time a pull request targets that branch or any branches contained under it. For example the pull request template named `feature.md` would be applied if a pull request targeted the `feature` branch or any `feature/*` branches.

Branch specific pull request templates must be saved in your repository in a folder named `pull_request_template\branches\`. The `pull_request_template\branches\` folder must be in one of the following folders in your repo:

- The root folder of the repo
- A folder named `.vsts` that is contained in the root folder of the repo
- A folder name `docs` that is contained in the root folder of the repo

For example, a branch specific pull request template that should apply to all pull requests into the `dev` branch would be name `dev.md` or `dev.txt` and located in one of the following locations.

- `<repository root>\pull_request_template\branches\`
- `<repository root>\.vsts\pull_request_template\branches\`
- `<repository root>\docs\pull_request_template\branches\`

Just like default pull request templates, multiple locations are provided to give you flexibility in where you store your branch specific pull request templates in your repo. When a pull request is created VSTS searches the previous folders in the order given for a branch specific pull request template, and uses the first one it finds. If no branch specific pull request template is found, VSTS then searches for a default pull request template as described in the previous section.

## Additional pull request templates

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




