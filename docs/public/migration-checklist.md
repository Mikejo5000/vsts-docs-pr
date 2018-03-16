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

Bug history, sensitive details

## Code

Bad words, credentials

>[!TIP]
> If you aren't comfortable exposing the entire repository, you can migrate the tip to another project.
> See the [instructions for a tip migration](#git-tip-only-migration).

## CI/CD

## Testing

## Reporting

## Extensions

Are any extensions vital to your project's experience?
For instance, do you have a control on your work item form which renders data in a particular way?
Are there custom hubs which expose important details?

* Check whether each extension's author has made it available for non-members by testing it.
* If not, ask the extension author to add support for non-members.

- Migrate just the tip of all Git repos, after ensuring nothing undesirable exists there 
- Copy any important bugs (maybe with the new WIMigrator tool?)
- Export and import build definitions 
 
# Partial migration tips

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