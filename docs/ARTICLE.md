# How to run a Strapi development environment in Google Cloud Shell using Ngrok

## Introduction

In this tutorial, you will learn how to install Strapi and run it on Google Cloud Shell.

After going through this tutorial, you will be able to use test and use Strapi on Google Cloud Shell. You will use a service called ngrok to help with previewing your app. You will effectively have an online testing environment for your Strapi app.

### What is Strapi?

[Strapi is the leading open-source headless Content Management System (CMS)](https://strapi.io). It is 100% Javascript, based on Node.js, and used to build RESTful APIs and GraphQL. It also has a cloud SAAS, ☁ [Strapi Cloud](https://strapi.io/cloud) ☁ - a fully managed, composable, and collaborative platform to boost your content velocity!

Strapi enables developers to build projects faster with a flexible and customizable platform for managing content. Check out the [Strapi Quickstart](https://docs.strapi.io/dev-docs/quick-start) guide for a brief intro.

One of the benefits of Strapi is that you can bootstrap an API in a matter of seconds.

### What is Ngrok?

[Ngrok](https://ngrok.com/) is an API-first ingress-as-a-service that simplifies connectivity, security, and observability for applications. It allows users to put their apps on the internet, connect to networks without complex configurations, and protect and scale their services with global network acceleration and load balancing. Ngrok is available as a single executable with no dependencies and can be used for both development and production environments.

Ngrok in this tutorial will help us preview the Strapi Admin Interface on port `1337`. Port `1337` is a restricted port on Google Cloud Shell, so having access to it is quite handy. Ngrok will work also help us to not meddle with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) settings in the Strapi app.

### What is Google Cloud Shell?

[Google Cloud Shell](https://cloud.google.com/shell/) is a free online development and operations environment accessible from any web browser. It provides command-line access to a Linux-based virtual machine instance. This machine comes preloaded with utilities and an online code editor with support for popular programming languages.

Cloud Shell offers a Virtual Machine Instance with the following features:
- 2 CPUs/4 CPUs
- 8GB/16GB of RAM
- 5GB of persistent disk storage in your `$HOME` folder
- 50 hours of weekly access

All in all Google Cloud Shell is a suitable environment to test out a Strapi app, especially if you are in a rush.

## Prerequisites

Before we begin, you need the following:

- [Google Account](https://accounts.google.com/)
- [Ngrok Account](http://ngrok.com/signup)
- Any Chromium-based browser

If you are in a rush, you can use the GitHub repo for this tutorial:
- [GitHub Repo Link](https://github.com/Marktawa/strapi-cloud-shell)

## Step 1 - Launch Google Cloud Shell

In your browser, log in to your Google Account and open up the Google Cloud Shell by visiting [shell.cloud.google.com](http://shell.cloud.google.com). This launches your Google Cloud Shell and you will see a window split into two with the **Cloud Shell Editor** on top and the terminal on the bottom.

In the terminal, you will see the following message, “*Welcome to Cloud Shell! Type “help” to get started.*”

![Google Cloud Shell Interface](https://cdn.hashnode.com/res/hashnode/image/upload/v1678099568337/8e6cb586-263a-44b5-be75-93c4ae1e3da6.png)

## Step 2 - Download Ngrok

To download ngrok, you first need to navigate to its official website at [https://ngrok.com/](https://ngrok.com/). Once you are on the website, click on the `Get started for free` button. This will take you to a page where you can [sign up for a free ngrok account](http://ngrok.com/signup).

![ngrok sign up form](https://cdn.hashnode.com/res/hashnode/image/upload/v1678099596055/82310ab1-1a96-4270-b21c-d917da0f3038.png)

After you have signed up, you will be redirected to the [ngrok dashboard](https://dashboard.ngrok.com/get-started/setup). Navigate to the [Setup & Installation](https://dashboard.ngrok.com/get-started/setup) page. From there, you can download the ngrok client.

![ngrok dashboard - setup & installation page](https://cdn.hashnode.com/res/hashnode/image/upload/v1678099681836/abab099a-0f39-4784-9d8f-8d88c384381e.png)

In our case, we want the **Linux** version of ngrok to use in Google Cloud Shell. Copy the link to the download. It should be similar to this - `https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz` depending on the latest stable version available.

In your Cloud Shell enter the following command:

```bash
cd $HOME
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
```

In a few seconds, the ngrok archive will be downloaded to your `$HOME` folder.

## Step 3 - Install Ngrok

After downloading ngrok, you will need to extract it. use the following command:

```bash
tar xvzf ngrok-v3-stable-linux-amd64.tgz
```

This creates a folder named `ngrok` in your `$HOME` directory.

Add `ngrok` to your PATH to execute the `ngrok` command.

```bash
sudo cp ngrok /usr/local/bin
```

Type `ngrok` in your shell to confirm it’s working.

```bash
ngrok
```

You should get an output similar to this:

![ngrok command output](https://cdn.hashnode.com/res/hashnode/image/upload/v1678099767700/a41a8290-bd9d-45ca-a780-3ff8fbc8f1e1.png)

Now that `ngrok` is working, the next step is to connect your Ngrok account.

## Step 4 - Connect Ngrok Account

Go to your Ngrok dashboard and navigate to [Your Authtoken - ngrok](https://dashboard.ngrok.com/get-started/your-authtoken). Copy your personal Authtoken.

Run this command to add your authtoken to the default `ngrok.yml` configuration file.

```bash
ngrok config add-authtoken <Authtoken>
```

> **NOTE**: *Replace with your specific ngrok account Authtoken*

This will authenticate the ngrok agent you downloaded in **Step 3**. It will also grant you access to more features and longer session times.

## Step 5 - Create Strapi App

Run the following command to install Strapi using the quickstart feature.
```bash
cd $HOME
npx create-strapi-app backend --quickstart
```
This creates your Strapi app in the folder named `backend`. The `quickstart` flag sets up your Strapi app with an [SQLite](https://www.sqlite.org/index.html) database.

After installation completes, your Strapi app should start running on port `1337`. 

![Strapi app running](https://cdn.hashnode.com/res/hashnode/image/upload/v1678133062194/fe2cbb28-4347-494e-a664-25e994054d29.png)

The next step requires `ngrok` for you to access Strapi's Admin UI in the browser.

## Step 6 - Run Ngrok

To connect to ngrok, open a new terminal tab by clicking the `+` icon in your Cloud Shell. Then run the following command:

```bash
cd $HOME
ngrok http 1337
```
This will start ngrok and create a public URL that you can use to access the Strapi app.

![ngrok running](https://cdn.hashnode.com/res/hashnode/image/upload/v1678133447294/046a8afe-4136-4862-b25b-38154f113f2a.png)

## Step 7 - Open Strapi App

Now that Strapi is running and ngrok is configured to forward requests to your Strapi instance, it's time to open up the Strapi app in your browser. Open up the link you have been assigned by `ngrok` in your browser. It's in the form `<unique-ngrok-subdomain>.ngrok.io`. You will see the **Welcome to your Strapi app** page.

![Welcome to your Strapi app page](https://cdn.hashnode.com/res/hashnode/image/upload/v1678133818119/9307b936-6b2b-449e-808a-be9beb9586a0.png)

Click **Create the first administrator** button to register an Admin user for your Strapi app.

![Strapi Admin Registration Form](https://cdn.hashnode.com/res/hashnode/image/upload/v1678134522431/a83b35a7-3955-405e-a94f-782720efb688.png)

After registering your admin, you will be redirected to the Strapi Admin Dashboard.

![Strapi Admin Dashboard](https://cdn.hashnode.com/res/hashnode/image/upload/v1678134881895/6b625126-45ad-43c0-8b74-2a5b7a37d5e6.png)

Here you can start creating collections and content for your Strapi app and publish your API when you're ready.

That's it.

If it is your first time working with Strapi, please check out [Strapi's Quick Start Guide](https://docs.strapi.io/dev-docs/quick-start) for a more in-depth tour.

## Conclusion

In conclusion, this tutorial has provided you with a step-by-step guide on how to run a Strapi development environment in Google Cloud Shell using Ngrok. You have learned how to install Strapi, launch Google Cloud Shell, and install Ngrok. 

You have also gained knowledge on what Strapi, Ngrok, and Google Cloud Shell are, and what they do. With this tutorial, you can easily create a testing environment for your Strapi app and preview it online using Ngrok.

### Useful Links

[Strapi Documentation](https://docs.strapi.io)

[Ngrok Documentation](https://ngrok.com/docs)

[Google Cloud Shell Documentation](https://cloud.google.com/shell/docs)

If you have any questions or comments, feel free to leave them below.