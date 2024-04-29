# How to Build a Secure and Decentralized Blog Website on the Blockchain

![blogwebsite](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/myblogwebsite.1350.648.PNG)

---
slug: How to Build a Secure and Decentralized Blog Website on the Blockchain
title: How to Build a Secure and Decentralized Blog Website on the Blockchain
image:https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/myblogwebsite.1350.648.PNG
authors: [samthetutor]
tags: [programming, development, internetcomputer]
---

## Introduction

In the digital realm's evolution, decentralized applications (dApps) and blockchain technology have emerged as transformative tools for content creators and developers. Beyond cryptocurrencies, blockchain offers enhanced security, transparency, and user control, making it an appealing option for building online platforms. Building a blog website on the blockchain presents content creators with the opportunity to establish a censorship-resistant space where they retain full ownership of their content and data.
This article will provide a comprehensive guide on constructing your inaugural blog website on the blockchain, focusing on the Internet Computer (ICP) protocol. The tutorial will cover setting up the development environment using juno, designing the blog's interface, and deploying the decentralized application directly onto the blockchain. By the end of this article, the reader should have the knolwedge to deploy their own website on the blockchain.

## Prerequisites

- Prior knowldge of working with HTML,CSS and JavaScript
- Prior knowledge of working with terminal or command line
- Prior knowledge of Github
- Prior kknowledge about Blockchain

## What is ICP

The Internet Computer (ICP) is a blockchain-based platform that aims to create a new type of internet, one that is decentralized, secure, and scalable. Developed by the Dfinity Foundation, the Internet Computer is designed to serve as a global public compute infrastructure, allowing developers to build and deploy decentralized applications (dApps) and services directly on the blockchain.
Unlike traditional blockchains, the Internet Computer uses a unique consensus mechanism called Threshold Relay, which allows it to achieve high transaction throughput and low latency. The platform is also designed to be highly scalable, with the ability to add more nodes and increase its computing power as demand grows. This makes the Internet Computer a promising platform for building a wide range of decentralized applications, from social media and e-commerce to finance and cloud computing.[Learn more about ICP](https://internetcomputer.org/)

## What is Juno

Juno is an open-source Blockchain-as-a-Service platform. It works just like traditional serverless platforms such as Google Firebase or AWS Amplify, but with one key difference: everything on Juno runs on the blockchain. This means that you get a fully decentralized and secure infrastructure for your applications, which is pretty cool if you ask me.

Behind the scenes, Juno uses the Internet Computer blockchain network and infrastructure to launch what we call a “Satellite” for each app you build. A Satellite is essentially a smart contract on steroids that contains your entire app. From its assets provided on the web (such as JavaScript, HTML, and image files) to its state saved in a super simple database, file storage, and authentication, each Satellite controlled solely by you contains everything it needs to run smoothly.
[Learn more about Juno](https://juno.build/)

## What are Github Actions

GitHub Actions is a powerful continuous integration and continuous deployment (CI/CD) platform that allows you to automate various software development tasks right within your GitHub repository. It enables you to build, test, and deploy your code automatically whenever certain events occur, such as a new commit, a pull request, or an issue being created. With GitHub Actions, you can create custom workflows that can perform a wide range of tasks, from running tests and building packages to deploying your application to a cloud platform. The platform provides Linux, Windows, and macOS virtual machines to run your workflows, and you can also use self-hosted runners to run your workflows on your own infrastructure. GitHub Actions simplifies the automation of your development processes, helping you to streamline your workflow and reduce the amount of repetitive code you need to write. [Learn more about Github Actions](https://docs.github.com/en/actions)

## About the Project

This is a simple blog website deployed on the internet computer blockchain using juno. It is integrated with Github Actions so that every time make changes to our project, they will automatically reflect on the live website

## Setting up the Project

In this section,we will cover how to setup a boilerplate project using juno's cli tool.

![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/firstss.600.338.gif)

Run the command below in your project terminal

```bash
npm create juno@latest
```

- Provide the name of the project `myBlog`

- Select the static/blog project

- Select `yes` to configure Github Actions. We will use this feature later on

- Select `no` to configure the local emurator. This is because we are not going to use it in this project

- Select `yes` to install the necessary npm dependencies.

## Creating a Juno Statellite

![juno statellite](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/createsatellite.600.338.gif)

The satellite will allow us to host and access our blog website on the internet.
To create a satellite, navigate to the [juno console](https://console.juno.build/) website

- Login with your internet Identity
- On the dashboard, select Launch new satellite
- Provide name `myBlogSatellite` for the satellite.
- Click `Create Satellite`

Once the satelitte is created, it is time to connect it to our project.

## Connecting the Project to the Satellite
![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/junobuildcli.600.338.gif)

We will use the `junobuild/cli` SDK package to login to the juno console account using the terminal and link the satellite to our project

```bash
npm i -g @junobuild/cli
```

Run the command above to download the package on your pc.

```bash
juno login
```

- This will prompt you to authorize the terminal to access your satellite from your juno console in your browser.

```bash
juno init
```

Running the above command will prompt you to select the `myBlogSatellite` as the satellite to connect to the project, specify `dist` as the folder that will hold our compiled files and finally select the language for the files.

## Project code

We are going to write our code for the project. It is a simple blog website where you can show the different articles you have written.
Open the project in your favorite code editor

### index.astro

Replace the code in the `index.astro` file inside the `pages` folder with the code below

```js
---
// Import necessary components and data
import blogPosts from '../components/blogPosts.json';
import Article from '../components/Article.astro';
import Background from "../components/Background.astro";
---

<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Blog</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.16/dist/tailwind.min.css" />
  </head>
  <body>
    <header class="bg-gray-800 text-white py-4">
      <nav class="container mx-auto flex justify-between items-center">
        <a href="/" class="text-xl font-bold">My Blog</a>
        <ul class="flex space-x-4">
          <li><a href="/" class="hover:text-gray-300">Home</a></li>
            <li><a href="*" class="hover:text-gray-300">Articles</a></li>
          <li><a href="*" class="hover:text-gray-300">About</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <div class="container mx-auto my-8">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {blogPosts.map((post) => (
            <Article
              title={post.title}
              image={post.image}
              description={post.description}
              url={post.url}
            />
          ))}
        </div>
      </div>
    </main>
    <Background/>
  </body>
</html>
```

In the above code, we display a navbar that has three tabs. We also display the data about the different blogs from our sample data store.

### Article.astro file

Replace the code in the `Article.astro` file with the code below

```js
---
interface Props {
  title: string;
  image: string;
  description: string;
  url: string;
}

const { title, image, description, url } = Astro.props;
---

<div class="bg-white shadow-md rounded-lg overflow-hidden">
  <a href={url} target="_blank">
    <img src={image} alt={title} class="w-full h-48 object-cover" />
  </a>
  <div class="p-4">
    <h3 class="text-xl font-bold mb-2">{title}</h3>
    <p class="text-gray-600 mb-4">{description}</p>
    <a href={url} target="_blank" class="text-blue-500 hover:text-blue-700">Read more</a>
  </div>
</div>
```

The code above displays information about a sigle blog like the title, decription and link to the main article

### blogPosts.json file

create a new file `blogPosts.json` file in the components folder and paste the code below
```json
[
    {
      "title": "Introduction to Astro",
      "image": "https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/download.300.168.png",
      "description": "Astro is a new static site generator that makes it easy to build fast, content-focused websites.",
      "url": "https://docs.astro.build/en/getting-started/"
    },
    {
      "title": "Tailwind CSS: A Utility-First CSS Framework",
      "image": "https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/tttttt.512.256.png",
      "description": "Tailwind CSS is a utility-first CSS framework that makes it easy to build responsive and customizable user interfaces.",
      "url": "https://tailwindcss.com/docs/installation"
    },
    {
      "title": "The Benefits of Static Site Generation",
      "image": "https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/staticsite.270.148.png",
      "description": "Static site generation offers several benefits, including improved performance, better security, and easier deployment.",
      "url": "https://www.netlify.com/blog/2016/05/02/top-ten-reasons-the-static-website-is-back/"
    }, {
        "title": "Introduction to Astro",
        "image": "https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/download.300.168.png",
        "description": "Astro is a new static site generator that makes it easy to build fast, content-focused websites.",
        "url": "https://docs.astro.build/en/getting-started/"
      }
  ]
```
This file holds our sample data for the blogs. Each blog has a title,description,image and a url to the original blog/article.

## Project Deployment
![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/junodeploy.600.338.gif)

```bash
npm run build
```

Run the above command in your project terminal to build and compile all the project files. The compiled files will be available in a new folder `dist`

```bash
juno deploy
```

Next, run the command above to deploy the project in the satellite `myBlogSatellite`. If the deployment is successful, the satellite url in the format `https://<SATELLITE_ID>.icp0.io` will be provided.You can use this url to access your project

![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/jjunodeploy.614.108.PNG)

## Setting up Github Actions

In this section, we are going to set up Github Actions for our project.
Every time we make changes to our project and push the code to our remote github repo, Github Actions will automatically update our satellite with the new changes. In that way, we dont have to manually redeploy the changes to the satellite everytime we make changes. [Learn more about Juno Github Actions](https://juno.build/docs/guides/github-actions)

### Generating secret token from the juno console
![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/createsecret.600.338.gif)

To set up Github Actions, we need a secret token that uniquely identifies our satellite.

- Visit [juno console](https://console.juno.build/), and select `myBlogSatellite` satellite.
- Under the controllers tab, click add controller
- Select 'Genetate new controller' and select 'Read-write' as the scope.
- Click submit.
Once the new controller is generated, it will provide a secret token, copy and store the secret token.

### Setting up Github Repo

![](https://a2ede-rqaaa-aaaal-ai6sq-cai.raw.icp0.io/uploads/addsecret.600.338.gif)

On your Github account, create a new repo and name it `myfirstBlog` and click create.

- On the settings tab, navigate to  `Secrets and variables` and click `Actions`.
- Click on the `new repository secret`, add `JUNO_TOKEN` as the name, paste the secret token you copied from the juno console in the `Secret` section.
- Click `Add secret`.


### Pushing Code to Github

We need to connect our local project to our remote github repo to be able to push our code there.

Run the command below in your project terminal

```bash
git init
git remote add origin https://github.com/sam-thetutor/myfirstBlog.git
git add .
git commit -m "my first commit"
git push -u origin main
```

This will connect your local project to the github repo we created, and everytime we push changes to this github repo, they will automatically be deployed to our satellite using the juno unique feature.

Now you have successfully deployed your first blog website on the blockchain, and every time you add a new article on your blog, Github Actions will automatically deploy the changes to your live website.

## Conclusion

In this article, we have looked at how to deploy your first blog website on the blockchain, how to create a juno satellite,how to link your satellite to your project and how to integrate Github Actions for continuous integration and continuous deployment (CI/CD).
