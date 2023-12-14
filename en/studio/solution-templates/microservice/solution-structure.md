# ABP Studio Microservice Solution Structure

This document explains the solution and folder structure of ABP Studio's [microservice solution template](index.md).

> This document assumes that you've created a new microservice solution by following the *[Quick Start: Creating a Microservice Solution with ABP Studio](../../quick-starts/microservice.md)* guide.

## Understanding the ABP Solution Structure

When you create a new microservice solution, you will see a tree structure similar to the one below in the *Solution Explorer* panel:

![microservice-solution-in-explorer](images/microservice-solution-in-explorer.png)

Each leaf item (e.g. `Acme.CloudCrm.IdentityService`, `Acme.CloudCrm.Web`, `Acme.CloudCrm.WebGateway`...) in the tree above is an **ABP Studio module**. An ABP Studio module can be a web application, an API gateway, a microservice, a console application or whatever .NET allows you to build. They are grouped into **folders** (`apps`, `gateways` and `services`) in that solution.

**Each ABP Studio module has a separate .NET solution**; this allows your team to develop them individually, in keeping with the nature of the microservices architecture.

> Refer to the *[Concepts](../../concepts.md)* document for a full definition of ABP Studio solution, module and package terms.

## Exploring the Folder Structure

You can write-click the root item in the solution explorer (`Acme.CloudCrm` for this example) and select the *Open with* -> *Explorer* command to open the folder containing the solution in your file system:

![open-solution-with-explorer](images/open-solution-with-explorer.png)

The root folder of the solution will be similar to the following:

![solution-folders](images/solution-folders.png)

The folder structure basically matches to the solution in ABP Studio's *Solution Explorer*:

* `.abpstudio` folder contains your personal preferences for this solution and it is not added to your source control system (Git ignored). It is created and used by ABP Studio.
* `app` folder contains the applications that has a UI and typically used by the end users of your system.
* `etc` folder contains some additional files for the solution. It has the following sub-folders:
  * `abp-studio` folder contains settings that are managed by ABP Studio. This folder is added to your source control system and shared between developers.
  * `docker` folder contains docker-compose configuration to easily run infrastructure dependencies (e.g. RabbitMQ, Redis) of the solution on your local computer.
  * `helm` folder contains all the Helm charts and related scripts to deploy the solution to Kubernetes.
  * `k8s` folder contains some additional files to setup *Kubernetes Dashboard* on your local machine.
* `gateways` folder contains one or more API Gateways (the count depends on if you've selected mobile application or other applications if available). This solution implements the [BFF](https://learn.microsoft.com/en-us/azure/architecture/patterns/backends-for-frontends) (Backend for frontend pattern), that means it has a dedicated API Gateway for each different UI application.
* `services` folder contains the microservices. The microservice count varies on the options you've selected during the solution creation. However, the following microservices are always included:
  * `adminstration` microservice is used to manage permissions, languages and other fundamental settings of the system.
  * `identity` microservice is used to manage users, roles and their permissions. It basically serves to the [Identity](../../../modules/identity.md) module's UI (and [OpenIddict](../../../modules/openiddict.md) module's UI, if selected).

The next section explains each of the components with more details.

## Exploring the Components of the Solution

The solution consists of various applications, API gateways and services. Let's get to know the purpose and structure of each of them.

### AuthServer

`Acme.CloudCrm.AuthServer` is the authentication server of the system. It is a single-sign-on point, which means all the applications are using it for user login. Once users login via an application, they don't need to enter credentials (username, password) again for the other applications in the same browser, until they logout from one of the applications.

The `AuthServer` application is also used by microservices as the Authority for JWT Bearer Authentication.

That application is mainly based on the [OpenIddict](../../../modules/openiddict.md), the [Identity](../../../modules/identity.md), and the [Account](../../../modules/account.md) modules. So, it basically has login, register, forgot password, two factor authentication and other authentication related pages.

### Maui

This is the mobile application that is built based on Microsoft's [MAUI framework](https://learn.microsoft.com/en-us/dotnet/maui). It will be in the solution only if you've selected the MAUI as your mobile application option.