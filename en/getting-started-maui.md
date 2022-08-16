# Getting Started with the MAUI

ABP Commercial platform provides a basic [MAUI](https://docs.microsoft.com/en-us/dotnet/maui/what-is-maui) template to develop mobile applications **integrated to your ABP based backends**.

## Run the Server Application

Run the backend application as described in the [getting started document](getting-started.md).

Open the `appsettings.json` in the `MAUI` project:

{{ if Tiered == "Yes" }}

* Make sure that `Authority` matches the running address of the `.AuthServer` project, `BaseUrl` matches the running address of the `.HttpApi.Host` project.

{{else}}

* Make sure that `Authority` and `BaseUrl` matches the running address of the `.HttpApi.Host` or `.Web` project.

{{ end }}

### Android

The emulator or a physical phone **cannot connect to the backend** on `localhost`. To fix this problem, we need to configure port mapping.

Open a command line terminal and run the [`adb reverse`](https://developer.android.com/studio/command-line/adb#forwardports) command to mapping the backend application port to a emulator. For example:

`adb reverse tcp:44305: tcp:44305`

> You should run the command after starting the emulator

## Run the Mobile Application

![Maui Home Page](images/maui-home-page.png)

When you click Login to the application button, it will redirects to the auth server login page and enter **admin** as the username and **1q2w3E*** as the password to login to the application:

![Maui User Page](images/maui-user-page.png)

The user page show you how to use CSharp client proxy to request backend API.

The application is up and running. You can continue to develop your application based on this startup template.