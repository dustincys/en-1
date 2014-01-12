---
layout: post
title: Install and Update R and Rstudio on Ubuntu
categories: [programming language, ubuntu]
tags: [r, configure, rstudio]
---

As we know, R language is a famous open source language, which have been widely applied in biology fields due to its strong and complete functions of drawing and statistical computering ability. And Rstudio is the most popular IDE for R language. Although R is very useful in statistics and data analysis, R language is not prefect in some parts, such as, some old packages cannot be compatible with new R version. However, the common problems you always met every time is that R language is hard to update on Ubuntu at once. Thus, I write this journal to solve this common issue, especially when the R 3.0.2 is coming soon! 

## The Whole Procedues of Updating R

- step 1: Update And Upgrade R on Your PC
- step 2: Install the Old or New R Version
- step 3: Uninstall Rstudio on Your PC And Reinstall It on Your PC
- step 4: Merge Previous Packages with the New Packages 

### 1. Update and Upgrade R on Your PC

Firstly, you should comfirm what the R verison you have on your PC and update or upgrade your PC environment for preparing your installation of new R version. these commands are displayed blow.

#### Check the Current R Version on your PC
```
$ R --version 
```
#### Update your PC environment
```
$ sudo apt-get update 
```
#### Upgrade your PC environment
```
$ sudo apt-get upgrade
```

### 2. Install the Old or New R Version
After checking out your PC environment, now you could install the new R version from [R](http://cran.rstudio.com/) homepage or old R version from [R Source](http://cran.r-project.org/sources.html). And you could decompress the R source code zip file on your PC.

#### Download And Unzip the R Source Code
```
$ wget http://cran.r-project.org/src/base/R-3/
$ tar xvfz R-3.0.2.tar.gz
```
#### Configure the Environment 
```
$ cd R-3.0.2
$ ./configure
```
After that

```
$ make
```
![](http://i.imgur.com/EsMVc44.png)

And check if it was installed correctly.

```
$ make check
```
#### Install R Under */usr/local/bin/* 

After that, you could install it at **/usr/local/bin/**.

```
$ sudo make install
```
After that, You could directly use it in your terminal and the new **Rstudio** also can identify the new R version you installed just now. And you should close this terminal and resart a new one, then tpye in 

```
$ R --version
```
Check the version if the new R version has already on your PC and you could see that below

![](http://i.imgur.com/8U6lsLp.png)

### 3. Uninstall Rstudio on Your PC And Reinstall It on Your PC

#### Uninstall Old Rstudio from Your PC

Open **Ubuntu Software Center** and find **Rstudio** and uninstall it from your PC

![](http://i.imgur.com/rFBcNzH.png)

#### Download the New Version of Rstudio

You can download the lastest **Rstudio** version from this [page](http://www.rstudio.com/ide/download/desktop).

![](http://i.imgur.com/pYhLnnw.png)

After that, you could reinstall it via **Ubuntu Software Center**. and it will automatically change to the R version that you have installed. Fortunately, you could see it as below.

![](http://i.imgur.com/gM70JYv.png)

### 4. Merge Previous Packages with the New Packages

## Other references

-[升级完R后如何快速安装所有安装过的包](http://pgfe.umassmed.edu/ou/archives/3113)
