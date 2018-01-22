---
title: Pull request workflow extensibility | VSTS & TFS
description: Pull request workflow extensibility using status and policy
ms.assetid: 6ba68828-c05d-4afa-b29f-9ca39be5a0ce
ms.prod: vs-devops-alm
ms.technology: vs-devops-git 
ms.manager: douge
ms.author: sdanie
ms.date: 01/26/2018
---

# Customize and extend pull request workflows with pull request status

#### VSTS 

[Pull requests](../pull-requests.md) are a great tool for facilitating code reviews and managing code movement within a repository. 
[Branch policies](../branch-policies.md) enforce code quality during the pull request process by establishing requirements that must be performed for every code change. 
The policies provided by VSTS enable teams to enforce many best practices related to reviewing code and running automated builds, but many teams have additional requirements and validations to perform on code. 

In this topic, you'll learn about pull request statuses and how they can be used to integrate in the PR workflow.

## Overview

Integrating into the PR workflow involves a few different concepts:

* Service hooks
* Pull request status
* Status policy
* Custom actions

## Service hooks

Any service that wants to integrate with pull requests will need to know when a new PR has been created or updated, so that the contents of the PR may be evaluated. 
[Service hooks](../../service-hooks/overview.md) enable external systems to be alerted when events occur in VSTS.
There are two event triggers for pull requests: - **pull request created** and **pull request updated**. 
Ensure that there are subscriptions for both of these events to receive notifications any time the code in a PR changes.

## Pull request status

Pull request status provides a way for services to associate simple success/failure type information with a pull request, using the [Status API](https://go.microsoft.com/fwlink/?linkid=854107). 
A status consists of four key pieces of data:

* **State**. One of the following predefined states: `succeeded`, `failed`, `pending`, `notSet`, or `error`.
* **Description**. A string that describes the status to the end user.
* **Context**. A name for the status - typically describing the entity posting the status.
* **URL**. A link where users can get more information specific to the status.  

Essentially, status is the way a user or service posts their evaluation about a pull request.
Did the changes meet the requirements? 
Where can I learn more about what I need to do to meet the requirements?

Let's look at an example. 
Consider a CI service that is required to build all code changes in a project. 
When that service evaluates the changes a pull request, it needs to post back the results of the build and tests. 
For changes that pass the build, a status like this might be posted on the PR:

``` json
{
    "state": "succeeded",
    "description": "CI build succeeded",
    "context": {
        "name": "my-ci-system",
        "genre": "continuous-integration"
    },
    "targetUrl": "http://contoso.com/CI/builds/1"
}
```

This status would be displayed to the end user in the PR Details view:

``` 
TODO: Screenshot of status section
```

The `state` is shown to the user using an icon (green check for `succeded`, red X for `failed`, etc.). 
The `description` is displayed next to the icon, and the `context` is available in a tooltip. 
When a `targetUrl` is applied, the description will be rendered as a link to the URL. 

### Updating status

A service may update a PR status for a single PR by posting additional statuses, only the latest of which is shown for each unique `context`. 
Posting multiple statuses helps users manage expectations.
For example, posting `pending` status is a good way to acknowledge to the user that a system has received an event and is starting work. 
Using an informative `description` can further help the user understand how the system is working:

* "Build queued"
* "Build in progress"
* "Build succeeded"

## Status policy

Using status alone, details from an external service can be provided to users within the PR experience. 
Sometimes, sharing information about a PR is all that is necessary, but in other cases PRs should be blocked from merging until requirements are met. 
Like the in-box policies, the **Status policy** provides a way for external services to block PR completion until requirements are met. 

Status policies are configured just like other [branch policies](../branch-policies.md). 
When adding a new status policy, the **name** of the status policy must be entered. 
This requires that a status of `succeeded` with the `context.name` matching the selected name must be present to complete PRs. 
An **Authorized account** can also be selected to require that a specific account has the authority to post status that will approve the policy.  

## Custom actions

In addition to predefined service hook events that can trigger the service to update PR status, it is possible to extend the status menu by using [VSTS extensions](../../extend/index.md) to give the trigger actions to the end user. For example, if status that corresponds to a test run can be restarted by the end user, it is possible to have a **Restart** menu item to the status menu that would trigger tests to run.

## Additional concepts

### Iteration status

When the source branch in a PR changes, a new "iteration" is created to track the latest changes. 
Services that evaluate code changes will want to post new status on each iteration of a PR. 
Posting status to a specific iteration of a PR guarantees that status applies only to the code that was evaluated and none of the future updates. 

Conversely, if the status posted applies to the entire PR, independent of the code, posting to the iteration may be unnecessary.  
For example, checking that the author (an immutable PR property) belongs to a specific group would only need to be evaluated once, and iteration status would not be needed.

When configuring the status policy, if iteration status is being used, the **Status expiration** should be set to expire **Immediately**. 
This further guarantees that the PR will not be able to be merged until the latest iteration has a status of `succeeded`.

See the REST API examples for posting status [on an iteration](https://docs.microsoft.com/en-us/rest/api/vsts/git/pull%20request%20statuses/create#on_iteration) and [on a pull request](https://docs.microsoft.com/en-us/rest/api/vsts/git/pull%20request%20statuses/create#on_pull_request).

### Policy applicability

Status policies can be conditionally required by using the **Policy applicability** options. 
There are two models for conditionally applying a status policy:

1. **Apply by default** (opt-out). 
With this option, all PRs are blocked from merging until `succeeded` status is posted. 
A PR can be marked exempt from the policy by posting a status of `notApplicable`, which will remove the policy requirement.  

2. **Conditional** (opt-in). 
When a PR is created, the policy does not initially apply.  Only after status has been applied is the policy enforced.

Together, these options can be used to create a suite of dynamic policies. 
A "master" policy could be set to apply by default while the PR is being evaluated for applicable policies. 
Then, as additional conditional policies are determined to apply (perhaps based on specific build output), status can be posted to make them required. 
The master policy could be marked `succeeded` when it is finished evaluating or could be dismissed by marking it `notApplicable`.

## Next Steps

Learn more about the [PR Status API](https://go.microsoft.com/fwlink/?linkid=854107) and check out the how-to guides:

* [Create a pull request status server with Node.js](https://go.microsoft.com/fwlink/?linkid=854108)
* [Use Azure Functions to create custom branch policies](https://docs.microsoft.com/en-us/vsts/git/how-to/create-pr-status-server-with-azure-functions)
* [Configure a branch policy for an external service](https://go.microsoft.com/fwlink/?linkid=854109)