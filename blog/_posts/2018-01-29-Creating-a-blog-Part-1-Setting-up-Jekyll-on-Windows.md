---
layout: post
title:  "Creating a blog - Part 1 - Setting up Jekyll on Windows"
date:   2018-01-29 11:46:54 +0100
categories: jekyll linuxsubsystem ruby windows blogging
---

# Creating a blog - Part 1 - Setting up Jekyll on Windows
## Introduction


There are so many blogging engines on the market today. One of the most frequently used is probably Wordpress. It is kind of easy to setup and you can achieve many things easily. So why not going with Wordpress? Well, to be honest, I don´t know. 

In the next weeks I will post a few blogposts where I descibre my journey to creating a new blog. This first part is about why I decided to use Jekyll and how we can get up and running with a example blog. We will do this on a Windows 10 system so that will be kind of a challenge since Jekyll is mostly made for Linux systems! We´ll see how this works out :)

## Requirements

So since I decided to NOT using any of the major platforms, I thought about if I could find a engine, that lets me host my blog without paying much.
I also wanted to have the code public available to anybode who wants to see how I did things and maybe sending PR to fix minor bugs. Another really important thing is to blog with Markdown, since it is kind of a defacto standard. I also don´t want to deal with hosting databases or any other serverside thing that I need to worry about.

So let us summarize these requirements:

- Free (or cheap) hosting
- Sourcecode public
- Possiblity of making PRs 
- Markdown based
- No databases
- No server

## GitHub pages

As most of you might now, it is possible to host webpages on GitHub. This can be made by creating a (free) GitHub repository and putting some code onto it. There is a Step-by-Step guide that describes how you can do this. You can find this guide [here](https://pages.github.com/).

If you scroll down to the very end of this site, you see another awesome information:

[![Blogging with Jekyll]({{ site.contenturl }}1_GithubPages_BloggingWithJekyll.png)]({{ site.contenturl }}1_GithubPages_BloggingWithJekyll.png)

So **Jekyll**... Hmm.. is that a thing? Ok let´s just check it with our list from above:

- Free (or cheap) hosting --- **Check**
- Sourcecode public --- **Check**
- Possiblity of making PRs --- **Check**
- Markdown based --- **Check**
- No databases --- **Check**
- No server --- **Check**

So it looks like we are good to go, but before starting let us take a closer look at **Jekyll**.

## Jekyll 

If you go to the Jekyll page (www.jekyll.com)  you can get a quick introduction that says the following:

> ## So what is Jekyll, exactly?
> Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like Markdown) and our Liquid renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

So reading through this text I think that this might be a perfect fit for what I plan to do :).

## Difficulties with Windows

Fully motivated I am jumping into the setup procedure and ... doo! This guide is mostly written for Linux. But there is a Getting started guide for Windows too! Pheww.. 

At the top of the page is the following information:

> #### Jekyll on Windows
>
> While Windows is not an officially-supported platform, it can be used to run Jekyll with the proper tweaks. This page aims to collect some of the general knowledge and lessons that have been unearthed by Windows users.

Wow. So Jekyll is not supported on Windows? Oh come on. There must be a way to get this on Windows. But I don´t want to setup a dual boot or create a virtual machine. But wait... hasn´t Microsoft released something in the past that let´s you do... oh yeah! 

## Linux Subystem

Microsoft introduced the new Linux Subystem at the Build Conference in 2016. As soon as they released it I tried getting my hands on it and it was stunning. It felt like a real Linux, but it was so easy to setup and also easy to integrate. 

In the past few months there have been a few changes made to the Linux Subsystem. In the past you had to enable some specific features, go ot cmd and enter `bash`. You then where able to setup the Linux Subsystem. 

Since the latest release of Windows 10, this has changed a bit and now if you head to your commandline and type in `bash`, you get the following message:

> Windows Subsystem for Linux has no installed distributions.
Distributions can be installed by visiting the Windows Store:
https://aka.ms/wslstore
Press any key to continue...

Ok? Hm.. so let´s head over to the Appstore and see what we got. So opening my browser. Pasting in https://aka.ms/wslstore. Hit enter and the Appstore opens. 

[![Appstore Linux Subsytem]({{ site.contenturl }}1_AppStore_LinuxSubsystems.png)]({{ site.contenturl }}1_AppStore_LinuxSubsystems.png)

Sweet! In the early days of Linux Subystem there was only **Ubuntu**. It looks like you have now the opportunity to use **openSuse** and a **SUSE Linux** system. Thats pretty cool, but for now I will go with **Ubuntu**. Installing it is as easy as installing an app on your mobile phone. 

Fine. After downloading and installing it (just takes a few minutes depending on your network connection), you can start the Linux Subsystem. When we open it the first time we get prompted to define a UNIX username and a password:

[![Linux Subsytem install]({{ site.contenturl }}1_LinuxSubsystems_Install.png)]({{ site.contenturl }}1_LinuxSubsystems_Install.png)

Ok. After typing a username and a password we are already to use the Linux subsystem and so we are also ready to get our blog up and running! For this purpose we need to install all the needed components and because of the Linux Subsystem we can do this as if we would do it on a Linux system! Isn´t that AWESOME?

## Installing Jekyll

In the next few minutes we are going to setup Jekyll to get up and running with it. We will go through the needed requirements and then install Jekyll itself. After that we should be good to create our blog :)

### Installing Requirements for Jekyll

Now that we have our Linux installed, we can use the original guide to setup the Jekyll engine. So what are the requirements that we need to meet?

- GNU/Linux, Unix, or macOS
- [Ruby](https://www.ruby-lang.org/en/downloads/) version 2.2.5 or above, including all development
- [RubyGems](https://rubygems.org/pages/download) 
- [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/) 

So let us go through these requirements step by step.

#### GNU/Linux, Unix, or macOS

Since we are running on the Linux subsystem this requirement is already fullfilled. Next one :)

#### Ruby

The whole Jekyll engine is based on **ruby** and therefore we need to get it into our system.

You can check if ruby is already installed by typing `ruby -v` into your bash. If it is not installed, we will se an error message. 

To install ruby we have to perform the following command:

```bash
sudo apt-get install ruby2.3-dev
```

If everything worked correctly, you should be able to perform `ruby -v` and see the installed ruby version.
 
For me the upper command failed at the first execution, with the following message:

> Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?

Ok. Let´s just do what bash is telling us. Type in the following command to probably fix this issue:

```bash
sudo apt-get update
```

After this command succeeded, let´s rerun the command to install ruby and verify that it worked. Performing `ruby -v` gives us the following:

> ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]

Alright! This looks good. So we got ruby installed successfully. Next one are **RubyGems**.

#### RubyGems

This one should be easy. If you installed ruby correctly, **RubyGems** should be available on your system already. You can verify this by executing `gem -v` in your bash. If you installed the version I mentioned earlier you should see the following response in your bash:

> 2.5.1

#### GCC & Make

In this step we will install **gcc** & **make**. If your system is already setup you maybe already installed the necessary components. You can verify this by performing the following statements:

- `gcc -v`
- `g++ -v`
- `make -v`

All of those need to return a valid version. For my Ubuntu version this is not already  installed so let´s see what we need to do to get this things onto our system.

Because of the fact, that these components are really often installed together, there is a meta package, that let´s you easily install all of them. You can find further information on this package under https://packages.ubuntu.com/xenial/build-essential.

To install this package, we again will use the known commands:

```bash
sudo apt-get install build-essential
```

This takes a while so grab a coffee or a cup of tea. You choose!

After a few minutes you can double-check if the needed things are installed with the three commands. All of them should give you information on the installed version and that means that we are ready :)

### Installing Jekyll engine

Ok. We´ve installed all the requirements. That was easier than I thought. Now we will install the Jekyll engine. Since we already setup **RubyGems** we will do the installation with the help of it. You can do this by just executing the following command in bash:

```bash
sudo gem install jekyll bundler
```
This command will install both, the jekyll engine itself and the bundler that let´s you build and bundle your blog.

To verify if everything is setup correctly we can use the following command:

```bash
jekyll --version
```

## Creating a first blog

After all the steps above we are now ready to create our first blog. First of all we have to decide if we want to work in the Linux Subystem only, or if we want to stay on our Windows system and just create the Blog with our Linux Subsystem. Because of the fact, that I am working with VS Code I will go with the second option.

So to create the blog in a folder that is accessable from my Windows System easily, I will create this blog in my GitHub Folder which is located in my userprofiles documents folder. You can navigate to this folder by:

```bash
cd /mnt/c/Users/<ubuntu.username>/Documents/GitHub
```

You will have to replace the <ubuntu.username> with your actual username in Ubuntu, which might be different from your windows username. Ok so now we are in the correct directory. To setup the initial structure we have to use the following command:

```bash
jekyll new myblog
```

After the command succeeded we can open the folder in VS Code and we will see the following structure.

[![Initial Blog Structure]({{ site.contenturl }}1_InitialBlogStructure.png)]({{ site.contenturl }}1_InitialBlogStructure.png)

Looks good. To get a first few on how this will look in the browser we can now navigate to the folder and call the bundler to bundle the blog and serve it with a basic http serve:

```bash
cd myblog
bundle exec jekyll serve
```

If everything went well, your bash should show the endpoint that lets you reach your new awesome blog. For me it is http://127.0.0.1:4000/. Opening a browser of your choice, navigate to the page and voilà:

[![Initial Blog]({{ site.contenturl }}1_Browser_InitialPage.png)]({{ site.contenturl }}1_Browser_InitialPage.png)

## Conclusion

As you´ve seen it is really easy to get up and running with a Jekyll Blog! There are some steps that need to be taken to get the Linux Subystem setup. So in the end we have Jekyll setup on a Windows Computer, can work on the Windows PC and run all the engine parts in our Linux Subsystem.  