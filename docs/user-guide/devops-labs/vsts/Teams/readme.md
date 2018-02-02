---
title: Microsoft Teams Integration (Collaborate, Communicate and Celebrate)
layout: page
sidebar: vsts
permalink: /labs/vsts/teams/
folder: /labs/vsts/teams/
---

Last updated:6/27/2017

## Overview

<a href="https://teams.microsoft.com/start">**Microsoft Teams**</a> is your chat-centered workspace in Office 365. Software development teams get instant access to everything they need in a dedicated
hub for teamwork, that brings your teams, conversations, content and tools from across Office 365 and Visual Studio Team Services together into one place.

> Note: This integration is currently available for Visual Studio Team Services (not Team Foundation Server).

## Pre-requisites

1. You should have Office365 account in order to integrate **Visual Studio Team Services** with **Microsoft Teams**.

2. Only VSTS accounts in the same organization (AAD tenant) can be used to integrate with your Microsoft Teams account.

**You can start a free trial if you don't have Office365 account from <a href="https://teams.microsoft.com/start">here</a>**

In this lab, you’ll learn about how **Visual Studio Team Services** integrates with **Microsoft Teams** to provide a comprehensive chat and collaboration experience, across your Agile and development work.

## Getting started with Microsoft Teams

1. Launch **Microsoft Teams** - you can either open the web app or download the app to your desktop from <a href="http://bit.ly/2ouq6eN">here</a>

   <img src="images/2.png" />

2. After launching the app, you will see the **General Team**.

   <img src="images/3.png" />

3. Start adding Teams by clicking on the bottom left on **Add Team** button.

   <img src="images/4.png" />

4. Hover your mouse to create a new team.

   <img src="images/5.png" />

5. Give a name for your team and description if needed. Select the privacy settings and click on **Next**.

   <img src="images/6.png" />

6. You should see the status when creating team.

   <img src="images/7.png" />

7. Add members for your team in order to get notify the events that occur and also start conversations with your team members.

   <img src="images/8.png" />

## Integrating Visual Studio Team Services with Microsoft Teams 

**VSTS** integration with Microsoft Teams provides a comprehensive chat and collaborative experience across the development cycle. Teams can easily stay informed of important activities in your VSTS team projects with notifications and alerts on work items, pull requests, code commits, build and release.

1. Click on ellipsis button for the **VSTS Team** that was created and select **Connectors**.

   <img src="images/9.png" />

2. Select **Visual Studio Team Services** and add.

   <img src="images/10.png" />

3. Select the following and click on **save**.

   - VSTS Profile
   - VSTS Account
   - Project
   - Team 
   - Event Type

   <br>

   <img src="images/11.png" />

4. You can see the list of connectors that are configured to your team from the configured section.

    <img src="images/24.png" />

5. Since VSTS is configured now all the events will be seen under the  conversations tab. The events can be set accordingly depending upon the needs like **Work Item Updates, Build Summary** etc.

    <img src="images/25.png" />

## Working with Kanban Board within the Microsoft Teams

Your Kanban board turns your backlog into an interactive signboard, providing a visual flow of work. As work progresses from idea to completion, you update the items on the board. Each column represents a work stage, and each card represents a user story (blue cards) or a bug (red cards) at that stage of work.

The Kanban board can be added using Tabs. **Tabs** allow team members to access your service on a dedicated canvas, within a channel or in user's personal app space. You can leverage your existing web app to create a great tab experience within Teams.

1. Click on **+** icon to add new tab and select **Visual Studio**

   <img src="images/13.png"/>

   <img src="images/14.png"/>

2. Select the account

   <img src="images/15.png"/>

   >Note: Only VSTS accounts in the same organization (AAD tenant) can be used to integrate with your Microsoft Teams account.


3. Select the desired account from the list and click on **continue**

   <img src="images/16.png"/>

4. You can see the **Kanban Board** appearing in the tab.

   <img src="images/17.png"/>

5. All the work can be monitored during the daily standup's and the updates are real when the work items states are changed. It also allows us to customize the Kanban Board from within the Teams and synced.

## Collaboration Experience

Messages are a good way to connect and keep a history of the conversation. It's even better to use emoji, stickers, and GIFs to make a great impression.

1. Start having conversations with your team members by selecting the **Conversations** tab.

   <img src="images/18.png" />

2. All the conversations could be retrieved at anytime without losing the history which helps the entire team to have a collaborative experience

3. Teams can have a collaborative experience with the latest updates with respect to the **work items, build summary** etc so that it helps in better transparency

## Working with Channels

Channels are key to organizing team collaboration. Name them by discussion topic, project, role, location, or for fun, so conversations and content are easy to find by everyone in the team.

Channels are the biggest “containers” within a Team and contain content & conversations pertaining to some theme. A Team can have many Channels, but a Channel only relates to a single Team.

1. Select the **Team** that was created earlier and click on **elipsis.**

   <img src="images/26.png" />

2. Give a name and description for your channel and click on **add.**

   <img src="images/27.png" />

3. Once the channel is created, the conversations can be started amongst the team members.

   <img src="images/28.png" />

## Sharing the Contents

Sharing the contents with team members is now easy with Microsoft Teams. You can attach any kind of document like **Word, PDF, GIF, Image** etc to make it easy for the teams to make sure that all are under one hood.

1. Click on **Files** and select **Upload** to share a document with the team

   <img src="images/19.png" />

2. Click on the document that was uploaded from the list to start editing and having a live conversation with your team members

   <img src="images/20.png" />

3. Share the related websites within the Teams as Tabs. Click on **+** and select **Website**

   <img src="images/21.png" />

4. Provide a name for the website and click on **save**. It appears on the channel where all of the team members can access to get a quick information if there were any updates done

   <img src="images/22.png"/>

5. This is how the website looks when added to the channel.

   <img src="images/23.png" />

   












