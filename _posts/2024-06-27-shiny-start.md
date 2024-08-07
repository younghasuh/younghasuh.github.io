---
title: "Getting started with your own Shiny app"
date: 2024-06-27
categories:
  - blog
---


<h1>Shiny App for Collections Data</h1>


From set up to deployment

Author: Young Ha Suh

Last updated: 6/27/2024

<h2>Setup and requirements</h2>


<h3>R and RStudio</h3>


**R** is a free, open-source programming language for statistical computing and data visualization. In the case of our app and collection data, it will be the main way we write the code needed to generate the application. Instructions for downloading can be found [here](https://www.r-project.org/) or [here](https://r4ds.had.co.nz/introduction.html#prerequisites).  

We will use R through **RStudio**, an integrated development environment (IDE) for R. Think of it as a more visual, user-friendly software for coding in R. It includes a console, syntax-highlighting editor that supports direct code execution, and tools for plotting, history, debugging, and workspace management. [Download here](https://posit.co/downloads/).

<h4>RStudio basics</h4>

While I won’t cover all the basics of RStudio here, it’s important to note certain components of the user interface. You can find more information [here](https://docs.posit.co/ide/user/ide/guide/ui/ui-panes.html).


* The **Source Pane** is where you can view and edit various code-related files (.R, .rmd, .txt). If there is more than one file open, you will see tabs that you can select through.
* The **Console** is where you can execute code. 
* The **Environments** are a set of tabs but the one that you’ll use the most is the first Environment tab which lists currently saved R objects such as tables or models. 
* The **Output Pane** also shows multiple tabs.
    * **Files** lists all the files in the folder or R project directory.
    * **Plots** displays various outputs such as plots or html content. 
    * **Packages** shows currently installed R packages and which ones are loaded in the current session. You can search or install/update packages here.
    * **Help** displays package documentation and vignettes, if you need to remember how a function works, for instance. 

![image32](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/4ad95831-336a-4e7b-825c-7a531e42215f)

<br>

<h4>Installing packages</h4>

Once R and Rstudio is downloaded, we will also need to install a few **packages** installed to run the script. Packages are extensions of R that contain code and documentation, often even sample data, that can be installed and used for various purposes. For instance:

```
install.packages("tidyverse") 
install.packages("leaflet")
install.packages(“urbnmapr”)
```

*note, urbnmapr might not be available for download. In that case, use the following to download the package through devtools. 

Packages need to be installed only** once**. After installation, you will need to **load** them to the current session. If you close RStudio and start it up again, you can skip the installation and  just load the packages, or libraries. Note that the library function does not require quotation marks.

```
# load libraries
library(tidyverse)
library(leaflet)
library(urbnmapr)
```

*Any lines that start with a # become **comments** – notes to yourself/others that won’t run in the console. It is good practice to use comments throughout your script to make sure your code is easily readable and anyone (including your future self) can know what certain lines of code does.

<h3>Shiny</h3>


**Shiny** is a package that makes it easy to build interactive web apps straight from R. To install and load the shiny package in R, open an R session and run
```
install.packages("shiny") 
library(shiny)
```

*More information about how to get started with shiny [here](https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/index.html). 

<h2>Using GitHub</h2>


Recommended reading: [Chapter 1 in Jenny Bryan’s Happy Git with R](https://happygitwithr.com/big-picture.html)

Additional reading: [Excuse me, do you have a moment to talk about version control?](https://peerj.com/preprints/3159/)

We will be using [GitHub](https://github.com/) as a way to store and share the necessary scripts and files needed to create the application. GitHub is a developer platform that allows developers (you!) to store, manage, and share code using Git, which is the software that provides [version control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control). 

Create a [GitHub account](https://github.com/signup) and [install git]([https://git-scm.com/downloads](https://git-scm.com/downloads)). 

<h3>Why do we need version control? </h3>


Version control simply means that the system records any changes to a file or set of files so you can recall certain changes. Basically, it is a detailed ‘track changes’ function for any files or scripts that you may edit but might want the backup copy of. In this instance, Git tracks changes of your files then GitHub stores them online by syncing to the cloud. Not only is it useful to have these backup copies, but it is also useful in recording who makes the different changes, allowing for more efficient collaborations since you can roll-back on previous versions or contribute to others’ work. 

<br>
<h3>Configure GitHub</h3>


Create a GitHub account and remember to note the username, email address, and the password. 

Go back to Rstudio, then install the necessary packages. We will use the “usethis” package. 
```
# install packages
install.packages("usethis")
library(usethis)

# set up git on your system
use_git_config(user.name = "myname123", user.email = "myname123@example.com")
```

Now we will confirm that RStudio and GitHub are communicating. 

In RStudio, select the ![image47](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/8581e4ae-44ee-4a03-a0dc-bf65930bdbab) logo on the top right (mine says test but yours is probably blank) then select “New Project”. Or, you can go to File > New Project… 

*Also, don’t worry if your RStudio looks different than my screenshots! You can change the appearance by going to Tools > Global Options > Appearance and select different Editor themes. 

![image40](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/cd2d17b6-3440-497a-b122-d4b9377d9f7c)

Once you click New Project, you will get a pop up with different options. Select Version Control. 

![image31](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/26a8a194-8998-4838-a17d-c0422613a2a5)

Since we are using Git, select Git.

![image2](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/37541117-fd46-47fb-8154-9d2657e850dd)

The fact that you can see these options means that Git/GitHub/RStudio are working! 

You will also see the options for Git on two spots, the top ribbon as well as the right pane next to Environment. 

![image21](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/88f68a73-fd6c-42d8-ac6a-f09cf42218f0)

<br>

<h3>Using GitHub for version control</h3>

There are 4 steps involved with syncing your local repository to the online one.  

![image20](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/9ca7b44d-b56c-4b08-bc93-c5aed0d4f114)

Basically, what happens on your local device does not automatically sync with the version stored online (GitHub). So in order to reflect any changes you made on your local machine need to get “pushed” to the cloud server OR any changes made on the cloud server needs to be “pulled” to your local machine to make sure the two are matched. This feature is essential if you are collaborating with other users that have their own local machines, but you can also view yourself (past or future) as one of these users in which Git/GitHub can keep track of any changes that are made. 

![image28](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/302c09e3-19c0-448b-a6b3-aaaf79e46e9e)

You always start with **pulling** to sync your local repository with what is in the cloud. This is particularly important if you are working on multiple devices (e.g., personal vs. work computers) or if there were any updates that happened to the remote repository. You can pull by clicking the down arrow in the Git tab on the top right corner. 

![image34](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/f902b069-9b41-4068-8331-3c59d5e94f5e)

Git will then tell you if there were any changes. The log message will provide some information on what changed. 

![image5](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/4be5954d-c3a4-4ebb-b50c-aefb66b4681a)

If everything is up to date, it will say so. This is where you always want to start. 

![image6](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/833368f7-3ea0-45bc-89c1-00fd251aad31)

Now you are ready to write or change any of the script. Whenever you edit something on your files, RStudio will tell you so by highlighting and adding an asterisk to the file that has the unsaved changes. In this example, I made changes to the server.R file and haven’t saved yet. 

![image17](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/a6d889df-b0d4-49aa-b317-3214cda233c5)

Once you save, then the asterisk disappears and the color returns. 

![image54](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/d11b8afb-0be1-416d-8bef-734e9419167c)

Once these changes are saved, your Git will indicate so as well by listing any changed and saved files. Here, I modified both the server.R and ui.R files.

![image52](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/8e81a4a2-3894-41dd-82a8-405a110e7a63)

Depending on what changes you make to the local repository, Git will identify the type of change by using the following symbols. 

![image10](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/898296fd-9ccc-4400-b3e4-fb6ebffe8fd5)

Next, we will **stage**, or select the files we want to sync to the remote repo. Usually, you’d want to stage every edit you make but it may not always be applicable. For instance, really large files may take a while to sync and you may want to do it directly on GitHub. Simply click the boxes to indicate which files you want to stage. 

![image4](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/15d2fc6a-4aa8-4ae8-881f-bb38c99d735e)

Once we select the files, we will **commit** them to the local Git with the commit button ![image23](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/feb3279a-124e-4992-8818-93ad80aa2d9c)

A new  “Review Changes” window will pop up. There are 3 key panels here.  

![image44](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/c498c32e-b0ff-49e7-8624-4572f79ffd79)

1. The top left panel lists all the files you are staging. If you want, you can skip the previous staging step and select the files you want to stage here. 
2. You want to write a short but comprehensive message here that explains what changes you’ve made you’re committing. Try to be more descriptive/specific than the example I provided! These notes will show on your GitHub page! 
3. The bottom half displays all the changes that have been made since the previous version. The old or deleted lines are in red and the new, modified lines are in green. This is a good way to review your work. You can check the changes for each staged file if you select it in the first panel. 

Basically, on this panel we are committing any changes we have made to be sent to the remote repo. This panel is fairly useful and you can do all the 4 steps here (pull - stage - commit - push). 

Once you are done, hit the Commit button. 

![image48](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/f04c2cc6-70b0-4169-91c6-42395975b672)

Git will then commit your changes to the remote repo. Again, it will describe what changes have been made. You can now close this window. 

![image55](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/54547923-a0d0-4d77-9639-e72f6f620125)

Last, we are finally ready to **push**! Once you commit, the “Review Changes” window should now be blank. Click on the up arrow that says Push. 

![image42](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/bf9038e9-b755-476a-b7e3-e8d0a421671f)

Depending on the size of the commit, R will process this command. Once you get the following message “HEAD -> main”, you’re good to go! 

![image8](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/7156cd24-89c0-427f-bb44-ed1d6569dd8a)

You can check any changes by going to the GitHub repo. This shows that the two files - ui.R and server.R - indeed were modified just a few minutes ago. You can also see what I wrote for the commits (and why it would’ve been useful to write something more descriptive). 

![image46](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/b3af07aa-a524-43d1-b71c-6032aca6d7ff)


Here comes the power/usefulness of GitHub. You can click on the Commits to see what changes have been made. 

![image24](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/c76c6da3-92d1-4fd3-8998-44d9471c5dff)

The Commits page will show you all the changes that have been made and when. 

![image30](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/4b34c4aa-b5de-4d83-ad50-d84e89d44e95)

You can click on each commit to see further details. If I click on the most recent commit (“Updated script”), GitHub will highlight all the changes. 

![image1](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/f7bc27b7-c169-4bfc-9786-1a8fa7feafd3)

For the instance of this app, any changes that I make will be pushed to the original remote repository. Those changes can be pulled to individual cloned repositories so the changes will reflect on different users’ repositories. While users can push their own changes to their own remote repositories, because they are working on clones (or **forked** repos), they cannot push their changes onto the original repository. Well, there are ways to push that I can either accept or reject, but we won’t get into that just yet. 

![image15](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/e800491b-e04e-4d2b-b115-4e978cbe2d7c)

GitHub has many other cool features. For instance, you can see who contributes which line of code for each file.  

![image38](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/6601696b-1729-475b-ae15-470195431a08)


You can also create [Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) that will help you keep track of your progress and collaborations! 


<br>

<h4>Merging conflicts</h4>


If the remote and local repositories are not synced (i.e., not at the same starting point), this will result in a **conflict**. You will likely receive an error message on where the conflict is and you will need to fix it to make sure the repositories are syncing properly. See more here: [https://happygitwithr.com/push-rejected.html](https://happygitwithr.com/push-rejected.html) 

Merging conflicts can be a PITA so I recommend to always PULL PULL PULL before you start working! And if you are working with a collaborator, communicate when you are working to prevent merging conflicts. 

Now we have the basics, we can clone the repository I made to your local computer. 


<br>

<h2>Cloning the repository</h2>

We will start by cloning my repository that has all the necessary script and files. Go to my [collectionsdata repository](https://github.com/younghasuh/collectionsdata). 

To clone this repository on your own computer, select the green <>Code button. 

![image14](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/69b849ed-5426-4cc0-87ab-5fba3c73ac0f)

![image13](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/0ae29c4f-0b42-4864-be05-89f7228b9c4d)

Use the clipboard function to copy the url in your clipboard. 

Now paste this copied url into RStudio. 

Remember when you created a new project and selected version control? Paste the copied url into the first line “Repository URL:” The Project directory name and subdirectory will autofill. Feel free to edit those as needed. Especially pay attention to where the project will be saved using the “Browse” button. Check the “Open in new session” to keep your current project open. 

![image3](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/cf97a1fa-456b-422e-b9c0-0da9f97aa0d3)

Once you hit “Create Project”, you will have essentially copied the same project I have shared on Github to your personal device. Take a minute to browse all the files in the directory (bottom right pane). Select the following R files: “app.R”, “server.R”, and “ui.R’ which will then show on your source pane. 

![image22](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/280123bb-01f8-426b-9eba-3f84b7d43daf)

<br>

<h2>Getting started in R</h2>


The entire script for the app is available in app.R. I will walk you through each part of the code. 

To run or execute each line of code, you can do it in 3 ways: 

1) run the script with **CTRL + Enter** at each line
2) highlight all lines of code you want to run then hit CTRL + enter, or
3) copy and paste the line in the Console then hit enter. 

First, load all the libraries after you install them once initially (e.g., `install.packages("here")`). Highlight the following script then use ctrl+enter to run then. In the console (bottom window), you can see the code run.
```
library(here)
library(shiny)
library(ggplot2)
library(tidyverse)
library(urbnmapr)
library(usmap)
library(leaflet)
library(sf)
```

Check if the working directory matches the folder that you saved the shiny app to. The file extension should match. If not, manually set the working directory with the `setwd()` function. Alternatively, you can go to Session > Set Working Directory > To Project Directory OR Choose Directory.
```
getwd()
#or
setwd("C:/Users/young/Documents/collectionsdata")
```
You should get something like [1] "C:/Users/young/Documents/collectionsdata". 

Next, we will load the data sets to run the script. For this example, use the following LACM data set that I’ve uploaded in GitHub. We will load this data into our working environment with the following. 
```
data <- read.csv(“data_2023.csv”)
```

The first step is to make your data become suitable for the written code, as in, we need to make sure the formatting and fields match. But before we do that, let’s load up the sample data first to see what we are working with. 
```
names(data)
names(data)[2] <- "catalog" 

head(data)
```

Alternatively, you can click on the object `data` in the Environment pane and it will load the data file on your source pane. But a few noteworthy points are:
* There are 124096 entries in this database
* There are 30 fields (columns) but the first one (“X”) can be ignored

![image11](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/d15bf9c3-192a-4784-8bc2-96ee5e7ca6a6)

Note that this data was exported from our EMu database as a csv format using Crystal Reports. 


<br>

<h3>Testing your app</h3>

First, split `app.R` into two files: `ui.R` and `server.R`. The `ui.R` file will have all the components of the `shinyUI` function and the `server.R `file will have all the components of `shinyServer()`.  Remember that in the `app.R` file, the ui and server were saved as individual objects in the environment, but for it to become a published app, we need to have them saved as two different files. 

See the following screenshot. Click the ![image25](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/3442820a-16fd-47fd-8683-13a144887dc7) “Run App” button next to the green arrow. It will basically use the ui.R and server.R files to generate the application. 

![image45](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/27844961-edd8-4afe-9874-fb54582f9cf1)

Alternatively, type the `runApp()` command on your console. Make sure that the shiny package is already loaded.
```
runApp()
```

Once that is done, there will be a popup window with the application! This window works as it would on a web browser. Explore what it can do by selecting a species and clicking through the tabs.

![image41](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/3b721df1-2383-46b6-b49d-3a1ef898c7fa)



<br>

<h2>Publishing the app</h2>


Read: 

[https://shiny.posit.co/r/getstarted/shiny-basics/lesson7/](https://shiny.posit.co/r/getstarted/shiny-basics/lesson7/) 

[https://shiny.posit.co/r/articles/share/shinyapps/](https://shiny.posit.co/r/articles/share/shinyapps/) 

Congratulations on your first application! Note that this app only runs on your system and is not publicly available. So, to allow anyone to use this application, we will share our shiny application as a webpage. Your users can navigate to your app through the internet with a web browser. They will find your app fully rendered, up to date, and ready to go.

We are going to use [shinyapps.io](shinyapps.io), Posit’s hosting service for Shiny apps.  

<h3>Using shinyapps.io</h3>

First, sign up and create an account. 

You can then access your Dashboard to see what apps are deployed. You can see my main application “lacm_birds” running online. 

![image9](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/3a267e6a-2f4f-49b0-aa52-33622e906fea)


<h3>Connecting with RStudio</h3>

Once your account is created, we need to configure the `rsconnect `package to use your account and the automatically generated token. In RStudio, install and load the rsconnect package.
```
install.packages('rsconnect')
library(rsconnect)
```

Return to your account on shinyapps.io and retrieve your token by clicking your avatar and selecting “Tokens”. 

![image53](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/426eec81-6388-4b0a-9321-2b355be2b009)

Now you can configure the rsconnect package to your account. 

Select the “Show” button on your token page. 

![image39](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/c88fb4fd-efae-490b-8ed5-a525f141ed1e)

A pop-up window will show and give you the option to copy the command to your clipboard. Copy this script with CTRL + C then paste it into the command line of RStudio and run. 

![image19](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/1d594800-53c0-46fc-869c-b0423442ddbf)


<h3>Deploying your app</h3>

<h4>Method 1: </h4>
Use the `deployApp` command from the rsconnect package. 
```
library(rsconnect)
deployApp()
```
The console will start running, starting with a message saying “Preparing for deployment. This may take a few minutes. Once it is done, you will see a message saying “Deployment complete” and “Successfully deployed to <https:// …..>

  ![image36](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/90c7e414-8dd4-40bd-8ba8-6d571bd86d6a)

<h4>Method 2: </h4>

From RStudio, launch your app using the `runApp()` or clicking on the ![image25](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/141fa475-691e-43e4-af2e-7d2ee67e067d) Run App icon. Once the app is launched in a separate window, select the Publish button.

![image16](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/26583494-0585-4443-b5fb-543f2128ccb0)

Once deployment is complete, your browser should automatically open. See the example [here](https://nhm-birds.shinyapps.io/collectionsapp/).

Alternatively, you can select the url produced in the console.

I usually have this link as a bookmark on my laptop and even phone so I can browse the collections database quickly and anywhere!

<br>

<h3>Updating your app</h3>
Say you wanted to add a feature or you noticed a bug in your application. You can easily make those changes in your R scripts then re-run the app to see if those changes have been made or errors have been fixed. Once you do, you will need to re-publish your app so that those changes will reflect on the server that it is hosted on. 

In RStudio, open the app. This time, you will see a “Republish” ![image12](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/1f6a3688-ecfb-4d93-abb4-810db8999b41) button. Click this and the following window will appear. Select the necessary components for the app – usually the data file, server.R, ui.R, and any dependencies (in this case, there is a logo image) then select “Publish”.

![image33](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/2af52f5f-caf0-4fd4-90bb-056413170d70)

R will get busy and the “Deploy” tab on the console will automatically start running. Give it a few minutes to fully run and the app should automatically launch on your browser once it is finished.

![image7](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/5d88ef94-9a46-4b27-8978-051ca1a84c3f)

Make sure to check if the new app is running smoothly with either the new changes or the errors fixed.

<br>

<h3>Troubleshooting</h3>

If you ever have problems launching your application, it can be helpful to see the message logs to understand what is causing the error. Some errors will be apparent during the deployment stage and any error messages will appear on the Deploy tab on the terminal. Alternatively, you can use the command `rsconnect::showLogs()` to show all the log messages of a deployed application. 

You can also go to the shinyapps.io dashboard and look at the logs there. Click the app you want to check (without clicking on the “open in new tab” ![image43](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/a1ffd25a-56c0-4847-9af7-54cb9b2279ec) icon).

![image26](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/81548b0c-35aa-46a3-a393-a76a53088a25)

It will show you some basic information about your app. 

![image18](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/8c4cdaea-a621-4ac2-a153-94e626fcd53d)

Select the Logs tab and it can also reveal what errors might be causing the issue. 

![image29](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/7420037d-8d9b-493b-9f69-4347012f2d2a)

<br>
<h3>Hosting multiple apps</h3>
You can host up to 5 applications on shinyapps.io with the free version. Here, you can see that I have 2 applications for my account. 

![image49](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/5189da18-2d06-4bac-b4b9-103d6246aa0a)

To avoid confusion, I set up separate R projects and separate shinyapps.io tokens. You can create a new token by selecting “Add Token” on the “Tokens” page on  your shinyapps.io page. Then you work through the same steps of using rsconnect to configure your new R project with shinyapps.io. 

Here is another app I made to compare two collections: [LACM and CUMV](https://nhm-birds.shinyapps.io/collectionsapp/). It is fairly similar to the one I made before but it contains LACM and CUMV data on just 4 species. I plan to build on this and combine more species and collections. 

![image35](https://github.com/younghasuh/younghasuh.github.io/assets/22403928/a8c5fc63-9aaa-4e6e-b4ed-68a4f5f79886)


**To be continued**
In the next post, I will explain how to edit the script to fit your data as well as workflows that can be adopted for your collections. 
