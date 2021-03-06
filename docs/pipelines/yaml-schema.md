---
title: YAML schema | VSTS
description: An overview of all YAML features.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 2c586863-078f-4cfe-8158-167080cd08c1
ms.manager: douge
ms.author: macoope
ms.reviewer: macoope
ms.date: 08/02/2018
monikerRange: 'vsts'
---

# YAML schema reference

Here's a detailed reference guide to VSTS YAML pipelines, including a catalog of all supported YAML capabilities, and the available options.
This document is intended for people who already have a strong understanding of YAML pipelines.

> The best way to get started with YAML pipelines is through the
[quickstart guide](get-started-yaml.md). 
> After that, to learn how to configure your YAML pipeline the way you need it to work, see conceptual topics such as [Build variables](process/variables.md) and [Phases](process/phases.md).

## Pipeline structure

Pipelines are made of one or more phases and may include resources and
variables. Phases are made of one or more steps plus some phase-specific data.
Steps can be tasks, scripts, or references to external templates.
This is reflected in the structure of the YAML file.

- Pipeline
  - Phase 1
    - Step 1.1
    - Step 1.2
    - ...
  - Phase 2
    - Step 2.1
    - Step 2.2
    - ...
  - ...

For simpler pipelines, not all of these levels are required. For example,
in a single-phase build, you can omit the container for "phases" since there
are only steps. Also, many options shown here are optional and have good
defaults, so your YAML definitions are unlikely to include all of them.


### Conventions

Conventions used in this topic:
* To the left of `:` are literal keywords used in pipeline definitions.
* To the right of `:` are data types. These can be primitives like **string** or references to rich structures defined elsewhere in this topic.
* `[` *datatype* `]` indicates an array of the mentioned data type. For instance, `[ string ]` is an array of strings.
* `{` *datatype* `:` *datatype* `}` indicates a mapping of one data type to another. For instance, `{ string: string }` is a mapping of strings to strings.
* `|` indicates there are multiple data types available for the keyword. For
instance, `phase | templateReference` means either a phase definition or a
template reference are allowed.

## Pipeline

```yaml
name: string  # name of the pipeline
resources:
  containers: [ container ]
  repositories: [ repository ]
variables: { string: string } | variable
phases: [ phase | templateReference ]
```

Learn more about [multi-phase pipelines](process/multiple-phases.md?tabs=yaml),
using [containers](#container) and [repositories](#repository) in pipelines,
and [variables](process/variables.md?tabs=yaml).

### Container

[Container phases](process/container-phases.md) let you isolate your tools and
dependencies inside a container. The agent will launch an instance of your
specified container, then run steps inside it. The `container` resource lets
you specify your container images.

```yaml
resources:
  containers:
  - container: string  # identifier (no spaces allowed)
    image: string  # container image name
    options: string  # arguments to pass to container at startup
    localImage: boolean  # whether to build the image locally instead of pulling from a registry
    endpoint: string  # endpoint for a private container registry
    env: { string: string }  # list of environment variables to add
```

### Repository

If your pipeline has [templates](#phase-template) in another repository, you must
let the system know about that repository. The `repository` resource lets you
specify an external repository.

```yaml
resources:
  repositories:
  - repository: string  # identifier (no spaces allowed)
    type: enum  # see below
    name: string  # repository name (format depends on `type`)
    ref: string  # ref name to use, defaults to 'refs/heads/master'
    endpoint: string  # endpoint for a GitHub repository
```

#### Type

Pipelines support two types of repositories, `git` and `github`. `git` refers to
VSTS Git repos. If you choose `git` as your type, then `name` refers to a repo
within the same project as the one you are building. Cross-project references are
not supported.

If you choose `github` as your type, then `name` is the full name of the GitHub
repo including the user or organization. For example, `Microsoft/vscode`. Also,
GitHub repos require a [service connection](library/service-endpoints.md)
for authorization.

## Phase

<!-- to be renamed job soon -->

A [phase](process/phases.md?tabs=yaml) is a collection of steps to be run by an
[agent](agents/agents.md) or, in some cases, on the server. Phases can be
run [conditionally](process/multiple-phases.md?tabs=yaml#conditions), and they
may [depend on earlier phases](process/multiple-phases.md?tabs=yaml#dependencies).

```yaml
- phase: string  # name of the phase, no spaces allowed
  displayName: string  # friendly name to display in the UI
  dependsOn: string | [ string ]
  condition: string
  continueOnError: boolean  # 'true' if future phases should run even if this phase fails; defaults to 'false'
  queue: string | queue
  server: true | server
  variables: { string: string } | [ variable ]
  steps: [ script | bash | powershell | checkout | task | stepTemplate ]
```

Learn more about [variables](process/variables.md?tabs=yaml). Also see
the schema references for [queue](#queue), [server](#server), [script](#script),
[bash](#bash), [powershell](#powershell), [checkout](#checkout), [task](#task),
and [step templates](#step-template).

> [!Note]
> If you have only one phase, you can use [single-phase syntax](process/phases.md?tabs=yaml)
> which omits many of the keywords here.

### Phase templates

Phases can also be specified in a phase template. Phase templates are separate
files which you can reference in the main pipeline definition.

```yaml
- template: string
  parameters: { string: any }
```

For example:

```yaml
# File: phases/build.yml

parameters:
  name: ''
  queue: ''
  sign: false

phases:
- phase: ${{ parameters.name }}
  queue: ${{ parameters.queue }}
  steps:
  - script: npm install
  - script: npm test
  - ${{ if eq(parameters.sign, 'true') }}:
    - script: sign
```

```yaml
# File: .vsts-ci.yml

phases:
- template: phases/build.yml  # Template reference
  parameters:
    name: macOS
    queue: Hosted macOS Preview

- template: phases/build.yml  # Template reference
  parameters:
    name: Linux
    queue: Hosted Linux Preview

- template: phases/build.yml  # Template reference
  parameters:
    name: Windows
    queue: Hosted VS2017
    sign: true  # Extra step on Windows only
```

See [template expressions](#template-expressions) for more about the `${{ }}`
syntax used here.

### In other repos

You can also put templates in a separate repository. In that case, you must
specify the [repository](#repositories) as a resource and then reference it
using `@`. For example:

```yaml
# File: steps/msbuild.yml
# Repository: https://github.com/contoso/example-templates

parameters:
  solution: '**/*.sln'

steps:
- task: msbuild@1
  inputs:
    solution: ${{ parameters.solution }}
- task: vstest@2
  inputs:
    solution: ${{ parameters.solution }}
```

```yaml
# File: .vsts-ci.yml
# Repository: https://contoso.visualstudio.com/MyProject/_git/MyRepo

resources:
  repositories:
  - repository: templates  # this name will be used after the '@' in the step
    type: github
    endpoint: my-github-endpoint
    name: contoso/example-templates
    ref: refs/tags/lkg
    
steps:
# This file will be pulled from the contoso/build-templates repository
- template: steps/msbuild.yml@templates
  parameters:
    solution: my.sln
```

Repositories are only resolved once, when the pipeline starts up. After that,
the same resource will be used for the duration of the build.

## Queue

`queue` specifies what [pool](agents/pools-queues.md) to use for a phase of the
pipeline. It also holds information about the phase's strategy for running.

```yaml
name: string  # name of the queue to run this phase in
demands: string | [ string ]  ## see below
timeoutInMinutes: number
cancelTimeoutInMinutes: number
parallel: number  # maximum number of agents to use at once when running this phase; also see `matrix`
matrix: { string: { string: string } }  ## see below
```

Learn more about [conditions](process/conditions.md?tabs=yaml) and
[timeouts](process/phases.md?tabs=yaml#timeouts).

### Demands

`demands` is supported by private pools. You can check for existence of a capability or a specific string like this:

```yaml
demands:
- myCustomCapability   # existence
- agent.os -eq Darwin  # specific string
```

### Matrix

`matrix` enables a phase to be run multiple times with different variable sets.
For example, a common scenario is to run the same build steps for varying
permutations of architecture (x86/x64) and configuration (debug/release).

For example:

```yaml
queue:
  matrix:
    x64_debug:
      buildArch: x64
      buildConfig: debug
    x64_release:
      buildArch: x64
      buildConfig: release
    x86_release:
      buildArch: x86
      buildConfig: release
steps:
- script: build arch=$(buildArch) config=$(buildConfig)
```

## Server

`server` specifies a [server phase](process/server-phases.md). It has many
of the same YAML properties as a normal `queue`.

```yaml
server: true
timeoutInMinutes: number
cancelTimeoutInMinutes: number
parallel: number  # maximum number of agents to use at once when running this phase; also see `matrix`
matrix: { string: { string: string } }  ## see `matrix` in the `queue` section
```

## Script

`script` is a shortcut for the [command line task](tasks/utility/command-line.md).
It will run a script using cmd.exe on Windows and Bash on other platforms.

```yaml
- script: string  # contents of the script to run
  displayName: string  # friendly name displayed in the UI
  name: string  # identifier for this step (no spaces allowed)
  workingDirectory: string  # initial working directory for the step
  failOnStderr: boolean  # if the script writes to stderr, should that be treated as the step failing?
  condition: string
  continueOnError: boolean  # 'true' if future steps should run even if this step fails; defaults to 'false'
  enabled: boolean  # whether or not to run this step; defaults to 'true'
  timeoutInMinutes: number
  env: { string: string }  # list of environment variables to add
```

Learn more about [conditions](process/conditions.md?tabs=yaml) and
[timeouts](process/phases.md?tabs=yaml#timeouts).

## Bash

`bash` is a shortcut for the [shell script task](tasks/utility/shell-script.md).
It will run a script in Bash on Windows, macOS, or Linux.

```yaml
- bash: string  # contents of the script to run
  displayName: string  # friendly name displayed in the UI
  name: string  # identifier for this step (no spaces allowed)
  workingDirectory: string  # initial working directory for the step
  failOnStderr: boolean  # if the script writes to stderr, should that be treated as the step failing?
  condition: string
  continueOnError: boolean  # 'true' if future steps should run even if this step fails; defaults to 'false'
  enabled: boolean  # whether or not to run this step; defaults to 'true'
  timeoutInMinutes: number
  env: { string: string }  # list of environment variables to add
```

Learn more about [conditions](process/conditions.md?tabs=yaml) and
[timeouts](process/phases.md?tabs=yaml#timeouts).

## PowerShell

`powershell` is a shortcut for the [PowerShell task](tasks/utility/powershell.md).
It will run a script in PowerShell on Windows.

```yaml
- powershell: string  # contents of the script to run
  displayName: string  # friendly name displayed in the UI
  name: string  # identifier for this step (no spaces allowed)
  errorActionPreference: enum  # see below
  ignoreLASTEXITCODE: boolean  # see below
  failOnStderr: boolean  # if the script writes to stderr, should that be treated as the step failing?
  workingDirectory: string  # initial working directory for the step
  condition: string
  continueOnError: boolean  # 'true' if future steps should run even if this step fails; defaults to 'false'
  enabled: boolean  # whether or not to run this step; defaults to 'true'
  timeoutInMinutes: number
  env: { string: string }  # list of environment variables to add
```

Learn more about [conditions](process/conditions.md?tabs=yaml) and
[timeouts](process/phases.md?tabs=yaml#timeouts).

### Error action preference
Unless specified, the task defaults the error action preference to `stop`. The
line `$ErrorActionPreference = 'stop'` is prepended to the top of your script.

When the error action preference is set to stop, errors will cause PowerShell
to terminate and return a non-zero exit code. The task will also be marked as
Failed.

Valid values are `stop`, `continue`, and `silentlyContinue`. For example:

```yaml
steps:
- powershell: |
    Write-Error 'Uh oh, an error occurred'
    Write-Host 'Trying again...'
  displayName: Error action preference
  errorActionPreference: continue
```

### Ignore last exit code

By default, the last exit code returned from your script will be checked and,
if non-zero, treated as a step failure. The system will prepend your script with:

`if ((Test-Path -LiteralPath variable:\LASTEXITCODE)) { exit $LASTEXITCODE }`

If you don't want this behavior, set `ignoreLASTEXITCODE` to `true`. 

```yaml
steps:
- powershell: git nosuchcommand
  displayName: Ignore last exit code
  ignoreLASTEXITCODE: true
```


## Checkout

`checkout` informs the system how to handle checking out source code.

```yaml
- checkout: self  # self represents the repo where the initial Pipelines YAML file was found
  clean: boolean  # whether to fetch clean each time
  fetchDepth: number  # the depth of commits to ask Git to fetch
  lfs: boolean  # whether to download Git-LFS files
```

OR

```yaml
- checkout: none  # skips checkout
```

## Task

[Tasks](process/tasks.md) are the building blocks of a pipeline. There is a
[catalog of tasks](tasks/index.md) available to choose from.

```yaml
- task: string  # reference to a task and version, e.g. "VSBuild@1"
  displayName: string  # friendly name displayed in the UI
  name: string  # identifier for this step (no spaces allowed)
  condition: string
  continueOnError: boolean  # 'true' if future steps should run even if this step fails; defaults to 'false'
  enabled: boolean  # whether or not to run this step; defaults to 'true'
  timeoutInMinutes: number
  inputs: { string: string }  # task-specific inputs
  env: { string: string }  # list of environment variables to add
```

## Step template

A single step can be defined in one file and used multiple places in another file.

```yaml
steps:
- template: string  # reference to template
```

For example:

```yaml
# File: steps/build.yml

steps:
- script: npm install
- script: npm test
```

```yaml
# File: .vsts-ci.yml

phases:
- phase: macOS
  queue: Hosted macOS Preview
  steps:
  - template: steps/build.yml # Template reference

- phase: Linux
  queue: Hosted Linux Preview
  steps:
  - template: steps/build.yml # Template reference

- phase: Windows
  queue: Hosted VS2017
  steps:
  - template: steps/build.yml # Template reference
  - script: sign              # Extra step on Windows only
```

## Template expressions

Template expressions enable values to be dynamically resolved during pipeline
initialization. A value that starts and ends with `${{ }}` indicates a
template expression.

Template expressions can expand variables and **template parameters**.
Parameters allow the caller to influence how a template is expanded.

For example:

```yaml
# File: steps/msbuild.yml

parameters:
  solution: '**/*.sln'

steps:
- task: msbuild@1
  inputs:
    solution: ${{ parameters.solution }}
- task: vstest@2
  inputs:
    solution: ${{ parameters.solution }}
```

```yaml
# File: .vsts-ci.yml

steps:
- template: steps/msbuild.yml
  parameters:
    solution: my.sln
```

### Functions

All general functions of [task conditions](https://go.microsoft.com/fwlink/?linkid=842996)
are available within template expressions.

Additionally, the following two functions are available:

* **format** - format a string. For example: `format('{0} Build', parameters.os)`
* **coalesce** - use the first non-null, non-empty string.
For example: `coalesce(parameters.restoreProjects, parameters.buildProjects)`

### Insertion

In addition to YAML values, you can use template expressions to influence the
structure of a YAML pipeline. For instance, to insert into a sequence:

```yaml
# File: phases/build.yml

parameters:
  preBuild: []
  preTest: []
  preSign: []

phases:
- phase: Build
  queue: Hosted VS2017
  steps:
  - script: cred-scan
  - ${{ parameters.preBuild }}
  - task: msbuild@1
  - ${{ parameters.preTest }}
  - task: vstest@2
  - ${{ parameters.preSign }}
  - script: sign
```

```yaml
# File: .vsts.ci.yml

phases:
- template: phases/build.yml
  parameters:
    preBuild:
    - script: echo hello from pre-build
    preTest:
    - script: echo hello from pre-test
```

When an array is inserted into an array, the nested array is flattened.

To insert into a mapping, you use the special property `${{ insert }}`.

```yaml
# Default values
parameters:
  variables: {}

phases:
- phase: build
  variables:
    configuration: debug
    arch: x86
    ${{ insert }}: ${{ parameters.variables }}
  steps:
  - task: msbuild@1
  - task: vstest@2
```

```yaml
phases:
- template: phases/build.yml
  parameters:
    variables:
      TEST_SUITE: L0,L1
```

### Conditional insertion

Finally, you can put this all together and conditionally insert into sequences
and mappings. For a sequence:

```yaml
# File: steps/build.yml

parameters:
  toolset: msbuild

steps:
# msbuild
- ${{ if eq(parameters.toolset, 'msbuild') }}:
  - task: msbuild@1
  - task: vstest@2

# dotnet
- ${{ if eq(parameters.toolset, 'dotnet') }}:
  - task: dotnet@1
    inputs:
      command: build
  - task: dotnet@1
    inputs:
      command: test
```

```yaml
# File: .vsts-ci.yml

steps:
- template: steps/build.yml
  parameters:
    toolset: dotnet
```

And for a mapping:

```yaml
# File: steps/build.yml

parameters:
  debug: false

steps:
- script: tool
  env:
    ${{ if eq(parameters.debug, 'true') }}:
      TOOL_DEBUG: true
      TOOL_DEBUG_DIR: _dbg
```

```yaml
steps:
- template: steps/build.yml
  parameters:
    debug: true
```

### Escaping

Prepend additional leading `$` characters to escape a value that literally starts and ends with `${{ }}`. For example: `$${{ }}`

<!--
## Syntax highlighting

Syntax highlighting is available for the pipeline schema via a VS Code
extension. You can [download VS Code](https://code.visualstudio.com),
[install the extension](https://example.com/TODO), and
[check out the project on GitHub](https://github.com/Microsoft/pipelines-vscode).
-->