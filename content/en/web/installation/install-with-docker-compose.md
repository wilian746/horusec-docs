---
title: Install with Docker Compose
weight: 10
description: In this section, you will find how to install Horusec web application in your environment using docker-compose.
---

## **What is it?**

[**Docker-Compose**](https://docs.docker.com/compose/)  is a tool to configure your application's services and also execute Docker applications in lots of containers. You can create and start all your configuration services with only one command. 

In this installation's case, the main goal is to use the Horusec's web application linked to your environment using Docker-Compose. 

{{% alert color="warning" %}} 
We don't recommend you to install Horusec using Docker-Compose in the production environment, for that [**install with Helm**]({{< ref path="/web/installation/install-with-helm.md" lang="en">}}) or [**Operator**]({{< ref path="/web/installation/install-with-operator/overview.md" lang="en">}}).
{{% /alert %}}


## **Requirements**
Check out the requirements in the [**Set up**]({{< ref path="/web/set-up.md" lang="en">}}) section. 


## **Configuration**
There is a **configuration file** on Horusec with all the default option for you to only configure your environment, in a simple and easy way. 
 
{{% alert color="info"%}}
This file can only be used for a testing scenario, never the production one.
{{% /alert %}}

- You can get the [**configuration file**](https://github.com/ZupIT/horusec-platform/blob/main/deployments/compose/compose.yaml) on Horusec's repository.

Follow the next steps to configure:
1. Clone the repository;
```bash
git clone https://github.com/ZupIT/horusec-platform.git

```

2. Enter the folder you have cloned

```bash
cd horusec-platform
```
3. Run the command `make install` in order to have all web applications.

```bash
make install
```


## **Access Horusec's services**

After you have done the previous steps, you can access the link to view the web application screens, showed by [**Horusec-Manager**]({{< ref path="/web/services/manager/introduction.md" lang="en">}}) service at [**http://localhost:8043**](http://localhost:8043).

 

{{% alert color="info" %}}
Remember, in the configuration file of this section, you will find all Horusec's services that will be exposed and executed in your machine.
{{% /alert %}}

For test cases, Horusec gives you a default e-mail and a password to access the platform:
```text
email: dev@example.com
password: Devpass0*
```

To change or disable the default user of the system just follow [our tutorial](/docs/tutorials/how-to-enable-disable-default-user)

{{% alert color="info" %}}
All backend services are exposed using **network_mode: "host"**, check if you have [**enabled Docker's configurations**](https://docs.docker.com/network/host/) to use this functions.
{{% /alert %}}


## **Images**
Horusec's images are available on [**dockerhub**](https://hub.docker.com/u/horuszup). You can check and use them. 

* [**horuszup/horusec-manager**](https://hub.docker.com/r/horuszup/horusec-manager)
* [**horuszup/horusec-auth**](https://hub.docker.com/r/horuszup/horusec-auth)
* [**horuszup/horusec-core**](https://hub.docker.com/r/horuszup/horusec-core)
* [**horuszup/horusec-api**](https://hub.docker.com/r/horuszup/horusec-api)
* [**horuszup/horusec-analytic**](https://hub.docker.com/r/horuszup/horusec-analytic)
* [**horuszup/horusec-migration**](https://hub.docker.com/r/horuszup/horusec-migration)
* [**horuszup/horusec-vulnerability**](https://hub.docker.com/r/horuszup/horusec-vulnerability)
* [**horuszup/horusec-messages**](https://hub.docker.com/r/horuszup/horusec-messages) (It is a requirement when you are using the [**e-mail service**]({{< ref path="/tutorials/how-to-enable-disable-messaging-service" lang="en">}})
* [**horuszup/horusec-webhook**](https://hub.docker.com/r/horuszup/horusec-webhook)

![](/docs/ptbr/web/installing/docker-compose/0-installing.gif)

## **Reminders**

{{% alert color="warning" %}}
1. All these configurations available on Horusec's [**docker-compose.yaml**](https://github.com/ZupIT/horusec-platform/blob/main/deployments/compose/compose.yaml) are default. It's recommended to change some information (like the user and database password) when using this service in a production environment.


2. Horusec always updates the images and performs corrections to know which image to use in specific versions. Check out [**release-notes**](https://github.com/ZupIT/horusec/releases) to see the correct versions for each service


3. There is [**a new access policy to download public dockerhub images**](https://docs.docker.com/docker-hub/download-rate-limit/). It is recommended to upload images in the register you want, to avoid any problems. 

4. When you enable the messaging service, it is necessary to connect to your e-mail service. For that, add to **"horusec-messages"** the following environment variables:   
- HORUSEC_SMTP_USERNAME="e-mail service username";
- HORUSEC_SMTP_PASSWORD="e-mail password service";
- HORUSEC_SMTP_ADDRESS: "e-mail address service";
- HORUSEC_SMTP_HOST: "e-mail host service";
- HORUSEC_SMTP_PORT: "e-mail service port".
{{% /alert %}}

### Read more
- [**How to use Horusec without Docker?**]({{< ref path="/tutorials/how-to-use-horusec-without-docker" lang="en">}})