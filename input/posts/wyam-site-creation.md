Title: Wyam website creation
Published: 03/07/2019
Tags:
- Introduction
- Wyam
- VSCode
---

This is my first post on my personal site.

I wanted to create a personal website to start documenting some of things that I mess about on and have interest in. Largely this will be development based I'm guessing but who knows. I went for a static site approach since I have no foreseeable need for dynamic content or proper backend. I'm initally hosting this on Azure Storage which has fairly recently started making this available.

So to start with I thought I'd create a simple post on how I'm going about creating my static website.

Being someone with more experience as a back-end developer than front-end I decided to use a static site creation tool. I chose Wyam [WYAM]: https://wyam.io/ over some of the more well known javascript based ones purely as it looked easy to use and extensible, with the added bonus it's written in dotnet. Wyam is 

> A HIGHLY MODULAR AND EXTREMELY CONFIGURABLE STATIC CONTENT GENERATOR AND TOOLKIT

After you have scaffolded a template project from one of the 'recipes', you can build your output html content with one of the themes, or create your own theme. You can also customise. Things such as posts can be written in markdown then translated into HTML when you build. Everything seems overrideable and customisable through concepts such as modules and pipelines. It includes support for using Razor views as well. Initially I have pulled down files the 'CleanBlog' theme.

I have been using VSCode for my IDE, which I've grown to love, and is always getting better with the ever growing list of handy extensions. 


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

That's it. Done. You should have a output folder complete with translated files. You can now preview the site using the Wyam preview server:

`wyam preview`

and navigate to http://localhost:5080

I chose to copy the theme files and Razor views from the wyam github repo so I could easily override behaviour and styles as required, and also because I find I learn more quickly if I can see how something is put together.

Any pipeline customizations can be done in the 'config.wyam' folder... I'll add examples as I need to start using them. As is stands I like how the site looks and how easy it was to put together.

## 


