---
title: ReadyToRun deployment overview
description: Learn what ReadyToRun deployments are and why you should consider using it as part of the publishing your app with .NET 5 and .NET Core 3.0 and later.
author: davidwrighton
ms.author: davidwr
ms.date: 09/21/2020
---
# ReadyToRun Compilation

.NET application startup time and latency can be improved by compiling your application assemblies as ReadyToRun (R2R) format. R2R is a form of ahead-of-time (AOT) compilation.

R2R binaries improve startup performance by reducing the amount of work the just-in-time (JIT) compiler needs to do as your application loads. The binaries contain similar native code compared to what the JIT would produce. However, R2R binaries are larger because they contain both intermediate language (IL) code, which is still needed for some scenarios, and the native version of the same code. R2R is only available when you publish an app that targets specific runtime environments (RID) such as Linux x64 or Windows x64.

To compile your project as ReadyToRun, the application must be published with the PublishReadyToRun property set to `true`.

There are two ways to publish your app as ReadyToRun:

01. Specify the PublishReadyToRun flag directly to the dotnet publish command. See [dotnet publish](../tools/dotnet-publish.md) for details.

    ```dotnetcli
    dotnet publish -c Release -r win-x64 -p:PublishReadyToRun=true
    ```

02. Specify the property in the project.

    - Add the `<PublishReadyToRun>` setting to your project.

    ```xml
    <PropertyGroup>
      <PublishReadyToRun>true</PublishReadyToRun>
    </PropertyGroup>
    ```

    - Publish the application without any special parameters.

    ```dotnetcli
    dotnet publish -c Release -r win-x64
    ```

## Impact of using the ReadyToRun feature

Ahead-of-time compilation has complex performance impact on application performance, which can be difficult to predict. In general, the size of an assembly will grow to between two to three times larger. This increase in the physical size of the file may reduce the performance of loading the assembly from disk, and increase working set of the process. However, in return the number of methods compiled at runtime is typically reduced substantially. The result is that most applications that have large amounts of code receive large performance benefits from enabling ReadyToRun. Applications that have small amounts of code will likely not experience a significant improvement from enabling ReadyToRun, as the .NET runtime libraries have already been precompiled with ReadyToRun.

The startup improvement discussed here applies not only to application startup, but also to the first use of any code in the application. For instance, ReadyToRun can be used to reduce the response latency of the first use of Web API in an ASP.NET application.

### Interaction with tiered compilation

Ahead-of-time generated code is not as highly optimized as code produced by the JIT. To address this issue, tiered compilation will replace commonly used ReadyToRun methods with JIT-generated methods.

## How is the set of precompiled assemblies chosen?

The SDK will precompile the assemblies that are distributed with the application. For self-contained applications, this set of assemblies will include the framework. C++/CLI binaries are not eligible for ReadyToRun compilation.

## How is the set of methods to precompile chosen?

The compiler will attempt to pre-compile as many methods as it can. However, for various reasons, it's not expected that using the ReadyToRun feature will prevent the JIT from executing. Such reasons may include, but are not limited to:

- Use of generic types defined in separate assemblies.
- Interop with native code.
- Use of hardware intrinsics that the compiler cannot prove are safe to use on a target machine.
- Certain unusual IL patterns.
- Dynamic method creation via reflection or LINQ.

## Cross platform/architecture restrictions

For some SDK platforms, the ReadyToRun compiler is capable of cross-compiling for other target platforms. Supported compilation targets are described in the following table.

| SDK platform | Supported target platforms |
| ------------ | --------------------------- |
| Windows X64  | Windows X86, Windows X64, Windows ARM32, Windows ARM64 |
| Windows X86  | Windows X86, Windows ARM32 |
| Linux X64    | Linux X86, Linux X64, Linux ARM32, Linux ARM64 |
| Linux ARM32  | Linux ARM32 |
| Linux ARM64  | Linux ARM64 |
| macOS X64    | macOS X64 |
