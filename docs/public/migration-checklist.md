---
title: Migration checklist
titleSuffix: Azure CodeX Public Project 
description: Best practices when changing a private project to a public project 
ms.technology: vs-devops-wit
ms.prod: vs-devops-alm
ms.assetid: 
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article
ms.date: 01/05/2018
---

# Migration checklist

**Azure CodeX Public Project**  

Most existing team projects contain a large amount of historical data.
Old work items, early commits, and previous build definitions might have content you aren't comfortable sharing publicly.
This checklist contains a list of things to think about before making a project public.
Also, it has ideas for migrating the latest state to a new project so that you can expose only current and future content.

## Agile

* Confirm that your work items, even closed ones, don't contain sensitive details: undisclosed security flaws, credentials, and customer data.
* Be aware that all discussions and descriptions are available. Check that none contain embarrassing or problematic speech.
* Confirm that none of your area paths have special, locked-down security settings. Denied permissions are not enforced in a public project, so these restricted area paths will become public.

>[!TIP]
> If you aren't comfortable exposing the whole work item database, you have migration options.
> See the [instructions for moving work items](#work-item-migration).

## Code

* Confirm that you have no sensitive details in your repositories' history: unpatched security bugs, credentials, and code you don't have the right to distribute.
* Be aware that all file contents and commit messages are available. Check that none contain embarrassing or problematic speech.

>[!TIP]
> If you aren't comfortable exposing an entire repository, you can migrate the tip to another project.
> See the [instructions for a tip migration](#git-tip-only-migration).

## CI/CD

* Confirm that none of your definitions exposes sensitive data: credentials/secrets, obscure URLs, and private environment names.
* Confirm that non-members don't require access to your private packaging feeds. Builds can still access feeds, but non-members cannot.

If you need to migrate build definitions to a new project (perhaps because you're moving code or work items), you can import & export using [YAML](../build-release/actions/build-yaml.md).

## Testing

* Understand that your manual testing and Cloud Load Testing features will not be available to non-members.

## Analytics & dashboards

* Consider building a dashboard intended for the public. Some [widgets are unavailable](feature-differences.md#analytics--dashboards) to non-members, so don't rely on these.

## Extensions

Are any extensions vital to your project's experience?
For instance, do you have a control on your work item form which renders data in a particular way?
Are there custom hubs which expose important details?

* Confirm that each extension's author has made it available for non-members by testing it.
* If not, ask the extension author to add support for non-members.
 
# Partial migration tips

## Work item migration

**TODO** talk about moving individual work items

**TODO** talk about WImigrator

## Git tip-only migration
You can do a tip-only migration if you don't want to share your repository's history.

>[!WARNING]
>The new repository will have no connection to the old one.
>You won't easily be able to migrate changes between them in the future.
>You should have all your developers switch to using the new repository.

- Clone the existing repository: `git clone <clone_URL>`
- Make sure you're in the root of the repository: `cd <reponame>`
- Ensure you're on the tip of the branch you want to start from, usually master: `git checkout master`
- Delete the Git data: `rmdir /s .git` on Windows, `rm -rf .git` on macOS or Linux
- Initialize a new Git repository: `git init`
- Create a new, empty repository in your public project.
- Add the new repository as your origin remote: `git remote add origin <new_clone_URL>`
- Push up your new repository: `git push --set-upstream origin master`