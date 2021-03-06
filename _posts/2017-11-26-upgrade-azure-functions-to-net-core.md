---
title: "Upgrade Azure Functions to .NET Core"
date: 2017-11-26 14:09:23 +0200
comments: true
categories:
  - quicktips
  - troubleshooting
tags: 
  - azurefunctions
  - dotnetcore
---

As of Visual Studio 2017 Preview 4, the Azure Functions tooling supports .NET Core by targeting .NET Standard. When
creating a new project you can select "Azure Functions v2" to get .NET Standard support.

![Net standard support](/images/NetStandardSupport.PNG){: .align-center}

However, there's currently no way to automatically migrate an existing Azure Functions project over to .NET Core. When opening an existing
full framework Azure Function project, these are the available framework targets:

![No standard framework available](/images/NoUpgradeForYou.PNG){: .align-center}

To upgrade to .NET Core you will have to manually edit the `.csproj` files to target the correct framework and add a version
element:

```
<PropertyGroup>
  <TargetFramework>netstandard2.0</TargetFramework>
  <AzureFunctionsVersion>v2</AzureFunctionsVersion>
</PropertyGroup>
```
After reloading the project, these options will available:

![Select net standard version](/images/CoreSelector.PNG){: .align-center}

### Set runtime version

If you already have a deployed version of the Azure function before the upgrade, you probably have to adjust the `FUNCTIONS_EXTENSION_VERSION` app settings value. Set it to `beta` to be able to use the .NET Core 2.0 runtime, as described [here](https://docs.microsoft.com/en-us/azure/azure-functions/functions-versions).

### Side note

.NET Standard does not support the `System.Configuration.ConfigurationManager` namespace, so any use of the ConfigurationManager needs to
be switched to either `Environment.GetEnvironmentVariable` or use the new configuration builder as described [here](https://blogs.msdn.microsoft.com/cjaliaga/2016/08/10/working-with-azure-app-services-application-settings-and-connection-strings-in-asp-net-core/).

![ConfigurationManager not supported](/images/NoMoreConfigurationManager.PNG){: .align-center}

Change from
`private static readonly string SlackWebhookUrl = ConfigurationManager.AppSettings["SlackWebhookUrl"];`

To
`private static readonly string SlackWebhookUrl = Environment.GetEnvironmentVariable("SlackWebhookUrl");`
