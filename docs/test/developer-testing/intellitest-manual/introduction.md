---
ms.assetid: A7B98509-7ACA-4E25-BD1B-BBC98742F028
title: Overview | Microsoft IntelliTest Developer Test Tool | Visual Studio
description: Overview of Microsoft Visual Studio IntelliTest developer testing tool
ms.technology: vs-devops-test-tools
ms.prod: vs-devops-alm
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Overview of Microsoft IntelliTest

[!INCLUDE [irm-pages-header-shared](../../_shared/irm-pages-header-shared.md)]

IntelliTest enables you to find bugs early, and 
reduces test maintenance costs. Using an automated 
and transparent testing approach, IntelliTest can 
generate a candidate suite of tests for your .NET 
code. Test suite generation can be further guided by 
*correctness properties* you specify. IntelliTest 
will even evolve the test suite automatically as the 
code under test evolves.

**Characterization tests**  
IntelliTest enables you to determine the behaviour of 
code in terms of a suite of traditional unit tests. 
Such a test suite can be used as a regression suite, 
forming the basis for tackling the complexity 
associated with refactoring legacy or unfamiliar code.

**Guided test input generation**  
IntelliTest uses an open code analysis and constraint 
solving approach to automatically generate precise 
test input values; usually without the need for any 
user intervention. For complex object types, it 
automatically generates factories. You can guide test
input generation by extending and configuring the 
factories to suit your requirements. Correctness 
properties specified as assertions in code will also be 
used automatically to further guide test input 
generation.

**IDE integration**  
IntelliTest is fully integrated into the Visual 
Studio IDE. All of the information gathered during 
test suite generation (such as the automatically 
generated inputs, the output from your code, the
generated test cases, and their pass or fail status) 
appears within the Visual Studio IDE. You can easily
iterate between fixing your code and re-running 
IntelliTest, without leaving the Visual Studio IDE. 
The tests can be saved into the solution as a Unit 
Test Project, and will be automatically detected 
afterwards by Visual Studio Test Explorer.

**Complement existing testing practices**  
Use IntelliTest to complement any existing testing 
practices that you may already follow.

If you want to test:

* Algorithms over primitive data, or arrays of primitive data:
  * write [parameterized unit tests](test-generation.md#parameterized-unit-testing)
* Algorithms over complex data, such as compiler:
  * let IntelliTest first generate an abstract representation of the data, and then feed it to the algorithm
  * let IntelliTest build instances using [custom object creation](input-generation.md#objects) and data invariants, and then invoke the algorithm
* Data containers:
  * write [parameterized unit tests](test-generation.md#parameterized-unit-testing)
  * let IntelliTest build instances using [custom object creation](input-generation.md#objects) and data invariants, and then invoke a method of the container and re-check invariants afterwards
  * write [parameterized unit tests](test-generation.md#parameterized-unit-testing) that call different methods of the implementation, depending on the parameter values
* An existing code base:
  * use Visual Studio's IntelliTest Wizard to get started by generating a set of [parameterized unit tests (PUTs)](test-generation.md#parameterized-unit-testing)

<a name="hello-world"></a>
## The Hello World of IntelliTest

IntelliTest finds inputs relevant to the tested 
program, which means you can use it to generate the 
famous **Hello World!** string. this assumes that 
you have created a C# MSTest-based test project and 
added a reference to **Microsoft.Pex.Framework**. If 
you are using a different test framework, create a C#
class library and refer to the test framework documentation
on how to set up the project.

The example below creates two constraints on the 
parameter named **value** so that IntelliTest will 
generate the required string.

```
using System;
using Microsoft.Pex.Framework; 
using Microsoft.VisualStudio.TestTools.UnitTesting; 

[TestClass]
public partial class HelloWorldTest {
    [PexMethod]
    public void HelloWorld([PexAssumeNotNull]string value) {
        if (value.StartsWith("Hello")
            && value.EndsWith("World!")
            && value.Contains(" "))
            throw new Exception("found it!");
    }
}
```

Once compiled and executed, IntelliTest generates a 
set of tests such as the following:

1. ""
2. "\0\0\0\0\0"
3. "Hello"
4. "\0\0\0\0\0\0"
5. "Hello\0"
6. "Hello\0\0"
7. "Hello\0World!"
8. "Hello World!"

Go [here](https://docs.microsoft.com/en-gb/visualstudio/test/generate-unit-tests-for-your-code-with-intellitest#Anchor_0)
to understand where the generated tests are saved.
The generated test code should include a test such as
the following:

```
[TestMethod]
[PexGeneratedBy(typeof(global::HelloWorldTest))]
[PexRaisedException(typeof(Exception))]
public void HelloWorldThrowsException167()
{
    this.HelloWorld("Hello World!");
}
```

It's that easy!

<a name="limitations"></a>
## Limitations

This section describes the limitations of IntelliTest:

* [Nondeterminism](#nondeterminism)
* [Concurrency](#concurrency)
* [Native .NET code](#native-code)
* [Platform](#platform)
* [Language](#language)
* [Symbolic reasoning](#symbolic-reasoning)
* [Stack traces](#incorrect-stack)

<a name="nondeterminism"></a>
### Nondeterminism

IntelliTest assumes that the analyzed program is 
deterministic. If it is not, IntelliTest will cycle
until it reaches an exploration bound.

IntelliTest considers a program to be non-determistic
if it relies on inputs that IntelliTest cannot control.

IntelliTest controls inputs provided to 
[parameterized unit tests](test-generation.md#parameterized-unit-testing)
and obtained from the 
[PexChoose](static-helper-classes.md#pexchoose). 
In that sense, results of calls to unmanaged or 
uninstrumented code are also considered as "inputs" 
to the instrumented program, but IntelliTest cannot 
control them. If the control flow of the program 
depends on specific values coming from these external
sources, IntelliTest cannot "steer" the program 
towards previously uncovered areas. 

In addition, the
program is considered to be non-determistic if the 
values from external sources change when re-running 
the program. In such cases IntelliTest loses control 
over the execution of the program and its search 
becomes very inefficient.

Sometimes it is not obvious when this happens. 
Consider the following examples:

* The result of the **GetHashCode()** method is 
  provided by unmanaged code, and is not predictable.
* The **System.Random** class uses the current system 
  time to deliver truely random values.
* The **System.DateTime** class provides the current 
  time, which is obviously not under the control of 
  IntelliTest.

<a name="concurrency"></a>
### Concurrency

IntelliTest does not handle multithreaded programs.

<a name="native-code"></a>
### Native code, .NET code that is not instrumented

IntelliTest does not understand native code, such as 
x86 instructions called through **P/Invoke**. It does
not know how to translate such calls into constraints
that can be passed to the 
[constraint solver](input-generation.md#constraint-solver). 
Even for .NET code, it can analyze only code it 
instruments. IntelliTest cannot instrument certain 
parts of **mscorlib**, including the reflection 
library. **DynamicMethod** cannot be instrumented. 

The suggested workaround is to have a test mode 
where such methods are located in types in a dynamic 
assembly. However, even if some methods are uninstrumented, 
IntelliTest will try to cover as much of the 
instrumented code as possible.

<a name="platform"></a>
### Platform

IntelliTest is supported only on the X86, 32-bit .NETframework.

<a name="language"></a>
### Language

In principle, IntelliTest can analyze arbitrary .NET 
programs, written in any .NET language. However, in 
Visual Studio it supports only C#.

<a name="symbolic-reasoning"></a>
### Symbolic reasoning

IntelliTest uses an automatic 
[constraint solver](input-generation.md#constraint-solver)
to determine which values are relevant for the test 
and the program under test. However, the abilities of
the constraint solver are, and always will be, limited.

<a name="incorrect-stack"></a>
### (Slightly) incorrect stack traces

Because IntelliTest catches and "rethrows" exceptions
in each instrumented method, the line numbers in 
stack traces will not be correct. This is a limitation
by design of the "rethrow" instruction.

<a name="further-reading"></a>
## Further reading

* [Introductory blog post](https://blogs.msdn.microsoft.com/visualstudioalm/2014/11/19/introducing-smart-unit-tests/) on MSDN.
* [Generate unit tests for your code with IntelliTest](https://docs.microsoft.com/en-gb/visualstudio/test/generate-unit-tests-for-your-code-with-intellitest)

[!INCLUDE [irm-help-support-shared](../../_shared/irm-help-support-shared.md)]

[!INCLUDE [irm-back-to-index-shared](../../_shared/irm-back-to-index-shared.md)]
