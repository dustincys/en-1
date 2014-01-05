---
layout: post
title: How to Install and Update R and Rstudio on Ubuntu
categories: [R language]
tags: [R, Configure, Programming Language, Basic Knowledge]
---

As we know, R language is a famous open source language, which have been widely applied in biology fields due to its strong and complete functions of drawing and statistical computering ability. And Rstudio is the most popular GUI for R language. Although R is very useful in statistics and data analysis, R language is not prefect in some parts, such as, some old packages cannot be compatible with new R version. However, the common problems you will often meet at your work is that R language is hard to update on Ubuntu at once. 

## The Whole Procedues of Updating R

- step 1: Update and Upgrade R on Your PC
- step 2: Install the Old or New R Version at Offical Website
- step 3: Uninstall Rstudio on Your PC And Reinstall It on Your PC

### 1. Update and Upgrade R on Your PC

Firstly, you should comfirm what the R verison you have on your PC and update or upgrade your PC environment for preparing your installation of new R version. these commands are displayed blow.

#### Check the Current R Version on your PC
```
$ R --version 
```
#### Update your PC
```
$ sudo apt-get update 
```
#### Upgrade your PC
```
$ sudo apt-get upgrade
```

### 2. Install the Old or New R Version at Offical Website
After checking out your PC environment, now you could install the new R version from [R](http://cran.rstudio.com/) homepage or old R version from [R Source](http://cran.r-project.org/sources.html). And you could decompress the R source code zip file on your PC.

#### Unzip the R Source Code Zip File

#### Configure the Environment 
```
$ ./configure
```
After that

```
$ make
```
![](http://i.imgur.com/EsMVc44.png)

And check if it installed correctly.

```
$ make check
```
#### Install R Under */usr/local/bin/* 
After that you could directly use it in the terminal

```
$ sudo make install
```
You could check the version if the new R version has already on your PC

```
$ R --version
```
And you could see that

![](http://i.imgur.com/8U6lsLp.png)

### 3. Uninstall Rstudio on Your PC And Reinstall It on Your PC

#### Uninstall Old Rstudio from Your PC

Open **Ubuntu Software Center** and find **Rstudio** and uninstall it from your PC

![](http://i.imgur.com/rFBcNzH.png)

#### Download the New Version of Rstudio from [Rstudio](http://www.rstudio.com/ide/download/desktop) Homepage

![](http://i.imgur.com/pYhLnnw.png)

After that, you could reinstall it and it will automatically change to the R version that you have installed. Fortunately, you could see below.

![](http://i.imgur.com/gM70JYv.png)
