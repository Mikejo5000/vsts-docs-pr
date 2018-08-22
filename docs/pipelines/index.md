---
title: CI/CD index to content for Azure Pipelines and Team Foundation Server | Azure Pipelines & TFS    
description: Learn how to configure CI/CD for the app and platform of your choice. Tutorials, references, and other documentation.  
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 00f4ed452-fbb8-45f9-8f0a-343702aac5b8  
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.reviewer: vijayma
ms.date: 02/19/2018
ms.topic: conceptual
layout: LandingPage
monikerRange: '>= tfs-2013'
---

::: moniker range="vsts"
# Pipelines
::: moniker-end
::: moniker range="< vsts"
# Build and release
::: moniker-end

::: moniker range="vsts"
Azure Pipelines help you implement a build, test, and deployment pipeline for any app.
Tutorials, references, and other documentation show you how to configure and manage continuous integration and delivery (CI/CD) for the app and platform of your choice.
::: moniker-end

::: moniker range=">= tfs-2015 < vsts"

[!INCLUDE [temp](_shared/concept-rename-note.md)]

Team Foundation Server (TFS) helps you implement a build, test, and deployment pipeline for any app.
Tutorials, references, and other documentation show you how to configure and manage continuous integration and delivery (CI/CD) for the app and platform of your choice.

::: moniker-end

::: moniker range=">= tfs-2015"

<table>
<tr>
<td>
Build GitHub projects
<td>
Your first build and release
</td>
<td>
Build a repo with YAML
</td>
<td>
Azure DevOps project
</td>
</tr>
</table>

### Learn how to build your app

<!-- Converting to icon48 format, this gets cleaner in YAML -->
<div class="ico48Case halfStack">
<div class="ico48Link"><a href="languages/android.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_android.svg"><span>Android</span></a></div>
<div class="ico48Link"><a href="apps/aspnet/build-aspnet-4.md"><img width="48" height="48" alt="" src="_img/index/logo_net.svg"><span>.NET</span></a></div>
<div class="ico48Link"><a href="languages/dotnet-core.md"><img width="48" height="48" alt="" src="_img/index/logo_net.svg"><span>.NET Core</span></a></div>
<div class="ico48Link"><a href="apps/c-cpp/gcc.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_Cplusplus.svg"><span>C/C++ with GCC</span></a></div>
<div class="ico48Link"><a href="apps/windows/cpp.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg"><span>C/C++ with VC++</span></a></div>
<div class="ico48Link"><a href="languages/docker.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_docker.svg"><span>Docker image</span></a></div>
<div class="ico48Link"><a href="apps/go/go.md"><img width="48" height="48" alt="" src="_img/index/logo_go.svg"><span>Go</span></a></div>
<div class="ico48Link"><a href="languages/java.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_java.svg"><span>Java</span></a></div>
<div class="ico48Link"><a href="apps/windows/dot-net.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_NET.svg"><span>.NET Desktop</span></a></div>
<div class="ico48Link"><a href="languages/javascript.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_nodejs.svg"><span>Node.js</span></a></div>
<div class="ico48Link"><a href="languages/python.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_python.svg"><span>Python</span></a></div>
<div class="ico48Link"><a href="apps/windows/universal.md"><img width="48" height="48" alt="" src="_img/index/logo_uwp.svg"><span>UWP</span></a></div>
<div class="ico48Link"><a href="languages/xamarin.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_xamarin.svg"><span>Xamarin</span></a></div>
<div class="ico48Link"><a href="languages/xcode.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_xcode.svg"><span>Xcode</span></a></div>
</div>

### Learn how to deploy your app

<!-- Converting to icon48 format, this gets cleaner in YAML -->
<div class="ico48Case halfStack">
<div class="ico48Link"><a href="targets/webapp.md"><img width="48" height="48" alt="" src="_img/index/app-service-web.png"><span>Azure Web App</span></a></div>
<div class="ico48Link"><a href="apps/cd/deploy-linuxvm-deploygroups.md"><img width="48" height="48" alt="" src="_img/index/virtualmachine.png"><span>Linux VM</span></a></div>
<div class="ico48Link"><a href="apps/cd/deploy-docker-webapp.md"><img width="48" height="48" alt="" src="_img/index/app-service-web.png"><span>Web App for Containers</span></a></div>
<div class="ico48Link"><a href="apps/cd/deploy-webdeploy-iis-deploygroups.md"><img width="48" height="48" alt="" src="_img/index/virtualmachine.png"><span>Windows VM</span></a></div>
</div>

### Learn how to test your app

<!-- Converting to icon48 format, this gets cleaner in YAML -->
<div class="ico48Case halfStack">
<div class="ico48Link"><a href="test/getting-started-with-continuous-testing.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg"><span>Visual Studio Test</span></a></div>
<div class="ico48Link"><a href="test/continuous-test-selenium.md"><img width="48" height="48" alt="" src="tasks/test/_img/visual-studio-test-icon.png"><span>Selenium Test</span></a></div>
<div class="ico48Link"><a href="test/review-continuous-test-results-after-build.md"><img width="48" height="48" alt="" src="tasks/test/_img/run-functional-tests-icon.png"><span>Review results</span></a></div>
</div>

## Step-by-step tutorials

* [CI builds for Git in Azure Pipelines](build/ci-build-git.md)
* [Set up multi-stage release](release/define-multistage-release-process.md)

## Videos

| | |
| --- | --- |
| <iframe src="https://channel9.msdn.com/Events/Connect/2017/T174/player" width="340" height="190" allowFullScreen frameBorder="0"></iframe> | <iframe src="https://channel9.msdn.com/Events/Connect/2017/T168/player" width="340" height="190" allowFullScreen frameBorder="0"></iframe> |
| <iframe src="https://channel9.msdn.com/Events/Connect/2017/T170/player" width="340" height="190" allowFullScreen frameBorder="0"></iframe> | <iframe src="https://channel9.msdn.com/Events/Connect/2017/T171/player" width="340" height="190" allowFullScreen frameBorder="0"></iframe> |
| <iframe src="https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/190/player" width="340" height="190" allowFullScreen frameBorder="0"></iframe> |
| | |

## Concepts

- [Release pipelines](release/index.md)
- [Build and release agents](agents/agents.md)
- [Build and release tasks](process/tasks.md)  
- [Licensing and build and release pipelines](licensing/concurrent-jobs-vsts.md)

## Resources

- [What is continuous integration?](/azure/devops/what-is-continuous-integration)  
- [What is continuous delivery?](/azure/devops/what-is-continuous-delivery)  
- [What is DevOps?](/azure/devops/what-is-devops)   
- [Build and release marketplace extensions](https://marketplace.visualstudio.com/search?target=VSTS&category=Build%20and%20release&sortBy=Downloads)
- [Manual and exploratory testing](../test/index.md)
- [Load and performance testing](../test/load-test/index.md)
- [Unit testing](https://docs.microsoft.com/visualstudio/test/unit-test-your-code)


<div id="main" class="v2">
    <div class="container">
        <h1>Azure Boards Documentation</h1>
        <p>Plan, track, and discuss work across your teams.</p>
        <p style="height: 30px;">&nbsp;</p>
        <ul class="pivots">
            <li>
                <a href="#index"></a>
                <ul id="index">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" style="display: none" href="#indexA" data-linktype="self-bookmark"></a>
                        <ul class="panelContent singlePanelContent" id="indexA" style="margin-top: 0px; display: flex; float: left; border: none;">
                            <li class="fullSpan">
                                <a href="#index1"></a>
                                <ul id="index1" class="cardsA cols cols4" style="float: left; display: flex;">
                                    <li>
                                        <a href="/vsts/boards/get-started/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="https://docs.microsoft.com/media/common/i_get-started.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Start using Azure Boards</h3>
                                                            <p>Sign up and get started using Azure Boards.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/work-items/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="https://docs.microsoft.com/media/common/i_tasks.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Work items</h3>
                                                            <p>Track code defects and user stories, capturing discussions along the way.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/boards/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_kanban.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Boards (Kanban)</h3>
                                                            <p>Manage the continuous flow of work from concept to completion.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/backlogs/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_backlog.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Backlogs</h3>
                                                            <p>Create and organize your backlogs, track features, users stories, and
                                                                bugs.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/sprints/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_scrum.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Sprints (Scrum)</h3>
                                                            <p>Plan a sprint, use a task board in daily scrums, monitor sprint burndown.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/queries/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_queries.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Queries</h3>
                                                            <p>Find work items to bulk update and to chart progress and trends.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/boards/plans/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_agile.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Plans and Agile at scale</h3>
                                                            <p>Grow your organization, support autonomous teams, and gain visibility
                                                                across teams.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/project/feedback/index">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="https://docs.microsoft.com/media/common/i_feedback.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Feedback</h3>
                                                            <p>Request and capture feedback on your working apps.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/organizations/settings/work/inheritance-process-model">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="/vsts/_img/index/i_config-tools.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Customization</h3>
                                                            <p>Configure tools and processes to meet your team's needs.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="/vsts/organizations/settings/about-settings#work">
                                            <div class="cardSize">
                                                <div class="cardPadding">
                                                    <div class="card">
                                                        <div class="cardImageOuter">
                                                            <div class="cardImage">
                                                                <img src="https://docs.microsoft.com/media/common/i_tools.svg" alt="" />
                                                            </div>
                                                        </div>
                                                        <div class="cardText">
                                                            <h3>Settings</h3>
                                                            <p>Configure resources for Azure Boards.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                </ul>
                                <a href="#index2"></a>
                                <h2 style="float: left; display: flex;">Additional resources</h2>
                                <ul id="index2" class="cardsL cols cols4" style="float: left; display: flex; width: 100%;">
                                    <li>
                                        <div class="cardSize">
                                            <div class="cardPadding">
                                                <div class="card">
                                                    <div class="cardText">
                                                        <a class="barLink" href="/vsts/index-all"><img src="https://docs.microsoft.com/media/common/i_library.svg" alt="" />Index</a>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </li>
                                    <li>
                                        <div class="cardSize">
                                            <div class="cardPadding">
                                                <div class="card">
                                                    <div class="cardText">
                                                        <a class="barLink" href="https://www.youtube.com/channel/UC-ikyViYMM69joIAv7dlMsA"><img src="https://docs.microsoft.com/media/common/i_video.svg" alt="" />DevOps at Microsoft</a>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </li>
                                    <li>
                                        <div class="cardSize">
                                            <div class="cardPadding">
                                                <div class="card">
                                                    <div class="cardText">
                                                        <a class="barLink" href="/vsts/articles/index"><img src="https://docs.microsoft.com/media/common/i_article.svg" alt="" />Technical articles</a>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </li>
                                    <li>
                                        <div class="cardSize">
                                            <div class="cardPadding">
                                                <div class="card">
                                                    <div class="cardText">
                                                        <a class="barLink"  href="https://docs.microsoft.com/en-us/azure/devops/learn/"><img src="https://docs.microsoft.com/media/common/i_dev-ops.svg" alt="" />Azure DevOps resource center</a>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </li>
                                </ul>
                            </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>

::: moniker-end

::: moniker range="tfs-2013"

**TFS 2013:** We recommend that you [Migrate from XAML builds to new builds](build/migrate-from-xaml-builds.md). If you're not yet ready to do that, then see [XAML builds](http://msdn.microsoft.com/library/ms181709%28v=vs.120%29.aspx).

::: moniker-end
