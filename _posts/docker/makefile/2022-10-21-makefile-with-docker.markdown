---
layout: posts
title:  "Make + Docker makes life easy"
last_modified_at:   2022-10-21 22:51:24 +1100
show_date: true
# header:
#   teaser: 
#   og_image:
#   image: https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/440px-Image_created_with_a_mobile_phone.png
#   caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories: blogs docker
tags: docker makefile make
readTime: 10 minutes
summary: 
categories:
  - Docker
tags:
  - docker
  - makefile
  - make
  - social
  - layout
  - table of contents
toc: true
toc_label: "Unique Title"
toc_icon: "heart"  # corresponding Font Awesome icon name (without fa prefix)
# sidebar:
#   - title: "Tiasdfastle"
#     image: "/assets/images/your-image.jpg"
#     image_alt: "image"
#     text: "Some text here."
#   - title: "Another Title"
#     text: "More text here."
#     nav: sidebar-sample
# excerpt: docker makefile make
---
Summary: Use the power of a makefile to reduce the load of typing big commands for docker interaction through docker cli.

## Problem 

When I work with docker commands, I don't remember all available syntax that I am going to use for day to day operations with docker cli, such as create image , run image etc.. .


As an example, let us say I have a defined this [nginx docker file](sample/Dockerfile) and my docker build command will be something like this: 

`docker build --file $(PWD)/Dockerfile --tag nginx:1.23.1-alpine_$(ENV) --build-arg env=$(ENV) .`

Now, every time I want to build my docker image, I will have to run this big docker command. 

So why should I waste my time, if I can simply type `make build` and it will build my docker image.

This is where `make` will be used.

## What is Make?

According to [this](https://gnuwin32.sourceforge.net/packages/make.htm) documentation  

*Make is a tool which controls the generation of executables and other non-source files of a program from the program's source files.*

## Solution

I will create a file called `makefile`. This file is a collection of targets. Each target contains a collection of commands that it will execute one after the another.
 
My target will look something like this: 

```
target: 
    @command1
    @command2
```

In the case of above given docker build example, I will define my target as 

```sh
build: 
	-@docker build --file $(PWD)/Dockerfile --tag nginx:1.23.1-alpine_$(ENV) --build-arg env=$(ENV) .
```

I can now call `make build` and it will execute the above big command for me.


Please have a look at a sample [makefile](makefile) you will find many commands that I have created to work with my nginx docker image.

![make help output](/assets/makefile-with-docker/makehelpoutput.png)  


Now this is the power of using make!


I can now build an image, run, check the status of my nginx container and status of my nginx configuration, with this single command: 

`make build start status testconfig` 

![final result](/assets/makefile-with-docker/finalresult.gif) 

Bingo! 

You have just replaced 4 big docker commands two 4 words.😆   

You can find my nginx sample code [here](/examples/docker-makefile-sample/) 