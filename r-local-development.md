---
title: "Local development R package"
Author: ["Simone Massaro", "Sam Herniman", "Anna Dodd"]
Date: 05 August 2025
---

# Outline

This document will guide you to make changes to your code following our recommended best practices, after your code has been updated by Pandion Labs. This document will attempt to get you started as quickly as possible. We will provide you with additional resources along the way so that you can learn more if you are interested.

1. Install IDE
2. Git & Github
3. First time setup
4. What's an R package?
5. Make a change
6. Publish the change
7. Additional resources

After following this document you will have all the necessary tools to do R development using the latest best practices.

The first 3 sections deal with setting up R, an IDE (RStudio or Positron), and git/github. If you have previously installed these, you may be able to skip these sections. This is a guide after all, no need to teach you things you already know.

## Why

Why do I have to go through all this trouble?

# 1. Install IDE

In order to properly edit your code it is best to use an IDE (Integrated Development Environment). There are many options available, for R development those are the two top options:

- Position (recommended)
- RStudio (legacy)

We suggest using Positron as it is the modern IDE with better features, but if you are used to RStudio it also works perfectly well.
Both of those editors are maintained by [Posit](https://posit.co/) (formerly RStudio), ensuring that they work well with R.

## Install R

- Our suggested way to install R is to use [rig](https://github.com/r-lib/rig), as it is a modern way to install R and manage multiple versions. 
- You need to first install rig, follow the [instructions](https://github.com/r-lib/rig?tab=readme-ov-file#%EF%B8%8F-installing-rig-) for your operating system
   - On Windows if you are using the installer method, Windows doesn't recognize the installer as safe. Rig can be totally trusted, so when you run it you should click on "more info" and then "run anyway"

::: {.panel-tabset group="ide"}

## Positron

- Go to [https://positron.posit.co/download.html](https://positron.posit.co/download.html) to download positron for your operating system. 
  - On windows if you have admin rights on your machine you can select the "system level install" other download "user level install"
- Follow the instructions to install positron
- In case of issues you can check the [Positron documentation](https://positron.posit.co/troubleshooting.html)
- Install R, in the terminal (a tab at the bottom section of your IDE) type `rig install`

## RStudio

- Open the terminal app (on windows the terminal is called `powershell`) and type `rig install`
- Go to [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)
- Ignore the step 1: Install R and directly go to step 2: Install RStudio
- Follow the instructions to install RStudio
- In case of issues you can check the [RStudio documentation](https://docs.posit.co/ide/user/)

:::


# 2. Git & Github

## Why Git

Git is a program that helps you track changes of your code versions and allows you to collaborate with others (like Pandion Labs) or colleagues. It takes a bit to setup but is well worth the effort.

### First concepts

Developers have a weird culture with its own language, but the concepts are not too hard once you get the hang of them. Here we've created a quick reference to translate "gitspeech"" into normal speech:

- **Repository**: This is a "folder" where your store code. 
- **Git vs GitHub**: Git is the program that runs on your computer and helps you keep track of your code versions, GitHub is a website where you can store your code and collaborate with others (Note: There are other websites that also serve a similar purpose, such as [GitLab](https://about.gitlab.com/)).

## Create a Github account

- Go to [https://github.com/join](https://github.com/join)
- Create an account and follow the instructions. Here are some [tips on how to choose your username](https://happygitwithr.com/github-acct#username-advice)
- **send your username to Pandion Labs**, so that you can be added to your repository

## Install Git on your computer

Another program you need to install! (Spoiler: This is actually the last one in this guide.)

::: {.panel-tabset}

### Windows/Mac OS

- Install [Github Desktop](https://desktop.github.com/)
- Log in with your github account

### Linux

- Use your package manager (i.e. `apt-get install git` or `dnf install git`)
- Install Git credential manager, it's pretty important to keep your sanity later to manage authentication with GitHub.
  - [Set the credential store](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/credstores.md#freedesktoporg-secret-service-api) by running
  ```bash
  git config --global credential.credentialStore secretservice
  ```
  - Install `.NET` on your machine, use [this guide](https://learn.microsoft.com/en-us/dotnet/core/install/linux)
  - Run in a terminal
  ```bash
  dotnet tool install -g git-credential-manager
  git-credential-manager configure
  ```
  to install git credential manager.


For additional details see the [official documentation](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md#net-tool)


:::

## Get your code

Now you need to clone (gitspeech for download) your repository (remember gitspeech for folder) onto your computer. It's important you use a new folder so that you have everything properly configured.

 1. Open Github Desktop
 2. `File -> Clone Repository`
 3. Search for your repository name
 4. Select the folder in your computer where you want to download your repository
 5. Click clone

![github desktop clone example](assets/github_desktop_clone.png)

# 3. First time setup

Congratulations! You have made it thought the difficult part, now everything will take place inside your IDE (integrated development environment -- i.e., RStudio/Positron).Speaking of which, the next step is to open your favorite IDE (either Positron or RStudio).

**Note**: For the first time you setup your package you will need to install the dependencies (i.e., all of R packages necessary to run your code).



## Familiarize yourself with the IDE

This is time to take a break and learn the basics of your IDE, here are our suggestions of what you have to know

::: {.panel-tabset group="ide"}

### Positron

- Check the [layout](https://positron.posit.co/layout.html)
  - Make sure you know how to navigate between files and folders
  - Understand the difference between the `console` and the `terminal`
- Keyboard shortcuts [https://positron.posit.co/keyboard-shortcuts.html#global-shortcuts](https://positron.posit.co/keyboard-shortcuts.html#global-shortcuts)
- [Data explorer](https://positron.posit.co/data-explorer.html)
- [Variables pane](https://positron.posit.co/variables-pane.html)
- [Help pane](https://positron.posit.co/help-pane.html)

### RStudio

- [Layout](https://docs.posit.co/ide/user/ide/guide/ui/ui-panes.html)

:::

## Open project

You want to open the folder that you cloned using GitHub desktop in the IDE

::: {.panel-tabset group="ide"}

### Positron

Press `Ctrl + Shift + P` and search for `File: Open Folder` and select the folder you cloned.

### RStudio

Go to `File -> New Project -> Existing Directory` and select the folder you cloned.

:::

## Install dependencies

::: {.callout-tip collapse="true"}
## No session in Positron

If in Positron you don't see any session, press `Ctrl + Shift + P` and search for `R: Select Interpreter` to set your R interpreter. Then it should start a new session.
:::

Go in the `console` on the top section (this is your friend - you will run a lot of your code there) and if everything worked you should see a prompt like this:

```bash
Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

>
```

then run

```r
renv::restore()
```

This will install all of your dependencies, it may take a few minutes.

# 4. What's an R Package

You can now start developing your project and start making changes. We recommend [this tutorial](https://r-pkgs.org/whole-game.html) in the _R Packages Book_ as an excellent way to learn everything you will need to know to build an R package.

## Code Structure

The code you will be working on is an R package. R packages follow a specific structure and conventions that help organize your code, data, documentation, and tests neatly.

Here is the typical structure you will see:

```bash
.
├── README.md          # Basic info about the package (automatically generated - don't edit this file)
├── README.Rmd         # Basic info about the package (editable)
├── R                  # This folder contains the main R code files defining functions
│   ├── data.R
│   ├── functions.R
│   └── utils.R
├── data               # Data files included in the package processed by R
│   └── data.rds
├── data-raw           # Original data that are then processed into the data folder
│   └── data.csv
├── man                # Documentation files auto-generated for package functions
│   ├── data.Rd
│   └── functions.Rd
├── vignettes
│   ├── articles       # Documentation that will go on the website
│   │   └── analysis1.Rmd      # Documentation that will go on the website
└── tests              # Automated tests to ensure your code works as expected
    ├── test-data.R
    └── test-functions.R
```

There are also other files and folders that you can ignore (but don't delete them!)

Don't worry if a lot of those folders don't make sense right now, we'll go through the important ones in the next sections.

## Functions

This is where most of the code lives, each individual function (or closely related functions) are in the file `R/<function_name>.R`. By organizing the code in this way we can split into components that are understandable and reusable.

An example of a function can be:

- `clean_data` which cleans the data to prepare for analysis
- `create_models` which creates all the statistical models needed for the analysis

If you want to add or change features in your core package functionality this is the place you will need to touch.


[Learn more about functions in R](https://r4ds.hadley.nz/functions.html)

## Notebooks

In the package there are `.Rmd` files in the `Readme.Rmd` and in the `vignettes/articles` folder. Those are R Markdown notebooks, which are a special type of files that combine

## Tests

**Every time**

# 7. Additional resources

- [https://happygitwithr.com](https://happygitwithr.com)
- [https://peerj.com/preprints/3159.pdf](https://peerj.com/preprints/3159.pdf)
