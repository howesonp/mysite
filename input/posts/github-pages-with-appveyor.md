Title: Website CD pipeline 
Published: 05/07/2019
Tags:
- GitHub Pages
- AppVeyor

---

#### AppVeyor and GitHub Pages

With my blog site created and viewable using the preview, next up was where to host it. Having created a GitHub repo for the project I decided to use GitHub Pages as the host primarily as it's free.

In order for me to make use of the site I really needed the process for adding content as pain free as possible so I set up a CD pipeline using AppVeyor.

There were a few things to set up first. The appveyor build task will use your input files in master and then output your site pages to another branch in your repo which will then be hosted. I created an orpaned branch for this on my main repo:

`git checkout --orphan gh-pages`

Then remove any content:

`git rm rf .`

before adding one 'dummy' file and pushing to the repo.

For the AppVeyor part create an account AppVeyor, linked it to the required GitHub repo by 'adding project', and granting to required access.

Then grab your personal access token from GitHub by

* Go to context menu top right of page
* Settings
* Developer Settings
* Personal Access Tokens
* Choose existing or generate new
* Copy to clipboard

Once you have the personal access token it can be encrypted using the encryption tool in AppVeyor before being added to the build script. Next time you push a commit to github your build will be kicked off. 

Not too tricky to setup and once it's working it saves so much time. Automation is good.

```
branches:
  only:
    - master
    
environment:
  access_token:
    # EDIT the encrypted version of your GitHub access token
    secure: 

install:
  - git submodule update --init --recursive
  - mkdir ..\Wyam
  - mkdir ..\output
  # Fetch the latest version of Wyam 
  - "curl -s https://raw.githubusercontent.com/Wyamio/Wyam/master/RELEASE -o ..\\Wyam\\wyamversion.txt"
  - set /P WYAMVERSION=< ..\Wyam\wyamversion.txt
  - echo %WYAMVERSION%
  # Get and unzip the latest version of Wyam
  - ps: Start-FileDownload "https://github.com/Wyamio/Wyam/releases/download/$env:WYAMVERSION/Wyam-$env:WYAMVERSION.zip" -FileName "..\Wyam\Wyam.zip"
  - 7z x ..\Wyam\Wyam.zip -o..\Wyam -r

build_script:
  - dotnet ..\Wyam\Wyam.dll --output ..\output

on_success:
  # Switch branches to gh-pages, clean the folder, copy everything in from the Wyam output, and commit/push
  # See http://www.appveyor.com/docs/how-to/git-push for more info
  - git config --global credential.helper store
  # EDIT your Git email and name
  - git config --global user.email "your email" $env:op_build_user_email
  - git config --global user.name "your user name" $env:op_build_user
  - ps: Add-Content "$env:USERPROFILE\.git-credentials" "https://$($env:access_token):x-oauth-basic@github.com`n"
  - git checkout gh-pages -f
  - git rm -rf .
  - xcopy ..\output . /E
  # EDIT your domain name or remove if not using a custom domain
  # - echo wyam.io > CNAME
  # EDIT the origin of your repository - have to reset it here because AppVeyor pulls from SSH, but GitHub won't accept SSH pushes
  - git remote set-url origin https://github.com/yourusername/yourreponame.git
  - git add -A
  - git commit -a -m "Commit from AppVeyor"
  - git push

```
