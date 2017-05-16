---
ms.assetid: 45777037-9E16-4ABF-BD26-5AF4E740D4E6
title: Settings waterfall | Microsoft IntelliTest Developer Test Tool | Visual Studio
description: Settings waterfall for Microsoft Visual Studio IntelliTest developer testing tool
ms.technology: vs-devops-test-tools
ms.prod: vs-devops-alm
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Settings waterfall

[!INCLUDE [irm-pages-header-shared](../../_shared/irm-pages-header-shared.md)]

The concept of the settings waterfall means that the 
user can specify settings at the **Assembly**, 
**Fixture** and **Exploration** level: 

* Assembly - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
* Fixture - [PexClass](attribute-glossary.md#pexclass)
* Exploration - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)

Settings specified at the **Assembly** level will affect all 
fixtures and exploration under that assembly. Settings 
specified at the **Fixture** level will affect all 
explorations under that fixture. Child settings win: 
if a setting is defined at the **Assembly** and the 
**Fixture** levels, the **Fixture** settings will be used.

Note that some settings are specific to the **Assembly** 
level or **Fixture** level. 

**Example**

```
using Microsoft.Pex.Framework;

[assembly: PexAssemblySettings(MaxBranches = 1000)] // we override the default value of maxbranches

namespace MyTests
{
    [PexClass(MaxBranches = 500)] // we override the 1000 value and set maxbranches to 500 
    public partial class MyTests
    {
        [PexMethod(MaxBranches = 100)] // we override again, maxbranches = 100
        public void MyTest(...) { ... }
    }
}
```

[!INCLUDE [irm-help-support-shared](../../_shared/irm-help-support-shared.md)]

[!INCLUDE [irm-back-to-index-shared](../../_shared/irm-back-to-index-shared.md)]
