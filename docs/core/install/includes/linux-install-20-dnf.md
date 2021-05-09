
### Install the SDK

The .NET Core SDK allows you to develop apps with .NET Core. If you install the .NET Core SDK, you don't need to install the corresponding runtime. To install the .NET Core SDK, run the following commands:

```bash
sudo dnf install dotnet-sdk-2.0
```

### Install the runtime

The .NET Core Runtime allows you to run apps that were made with .NET Core that didn't include the runtime. The following commands install the ASP.NET Core Runtime, which is the most compatible runtime for .NET Core. In your terminal, run the following commands.

```bash
sudo dnf install aspnetcore-runtime-2.0
```

As an alternative to the ASP.NET Core Runtime, you can install the .NET Core Runtime, which doesn't include ASP.NET Core support: replace `aspnetcore-runtime-2.0` in the previous command with `dotnet-runtime-2.0`.

```bash
sudo dnf install dotnet-runtime-2.0
```
