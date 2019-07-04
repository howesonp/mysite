Title: Wyam website creation
Published: 03/07/2019
Tags:
- Introduction
- Wyam
- VSCode
---
This is my first post on my personal site.


I wanted to create a personal website to start documenting some of things that I mess about on and have interest in. Largely this will be development based I'm guessing but who knows. I went for a static site approach since I have no foreseeable need for dynamic content or proper backend. I'm initally hosting this on Azure Storage which has fairly recently started making this available.

So to start with I thought I'd create a simple on going 'how to' series on how I'm going about creating my statically hosted website in Azure.

Being someone with more experience as a back-end developer than front-end I decided to use a static site templating tool. I chose Wyam over some of the more well known ones purely as it looked easy to use and completely extensible, which is even better since it's written in dotnet. The approach Wyam takes is to give some /input files, and pipelines to create an /output directory where all the input files are translated into proper html with 'themes' (which can be customised) are applied. The input files for blog posts etc can be written in markdown then translated. Everything is overrideable and it includes support for using Razor views as well.

I have been using VSCode for my IDE, which has provided a fantastic experience with the ever growing list of handy extensions. ... to do provide a list..


## Prerequisites

1. dotnet core and cli tools installed.
2. vscode installed

### Steps to install Wyam

- Start a terminal session in VsCode (assuming you have dotnet core cli installed) 
  `dotnet tool install -g Wyam.Tool`

### Steps to create the 'hello world' vanilla blog site

`wyam new --recipe Blog`

This will create the new site with the blog recipe, then you can edit the input files as required before building the blog with a certain theme:

`wyam --recipe Blog --theme CleanBlog`

That's it. Done. You should have a nice output folder with translated files

Any pipeline customizations can be done in the 'config.wyam' folder... I'll add examples as I need to start using them.

## Azure Static Website


Initially I am hosting this on Azure Storage using Static Website, however I'm already tempted by the ease of using GitHub Pages, so this may well change. Setting up Azure Storage was however pretty straight forward and the extension 'Azure Account' and 'Azure Storage' made deploying the site straightfoward.

