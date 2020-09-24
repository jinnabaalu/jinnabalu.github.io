---
layout: post
title:  "What is containerization and How does docker helps for a dev and prod environments"
description: "what problems Docker is meant to solve and start using Docker with containerization"
author: jinna
categories: [ Application ]
image: assets/images/docker.svg
---


In the beginning let me give you my short and concise definition of the problem Docker is built to solve. So we’ll start from there and move on step by step.

## What problem does docker solve?

This is the fundamental question of everyone who wants to start out with Docker. Let’s answer the question in the clearest and simplest way possible, with everyday words, not Docker terminology.

*What problem does Docker solve?* Docker solves the problem of having identical environments across various stages of development and having isolated environments for your individual applications.

The problem itself is as old as software development. Environment setup and management is a tedious task in every project.

In the old days we used custom scripts for that. We used to host various different applications on the same physical machine without any virtualization. It was usually a configuration nightmare to juggle with environment variables, trying to keep applications independently configurable or using two different versions of the same technology (like Java) on the same machine.

It used to be common practice to run your production applications on dedicated machines, while development or test environments were clattered with a lot of different applications to save hardware cost. In these cases your development and test servers were configured much differently than your production server.

Our infrastructure teams used to create different environment scripts for different stages, like development, test, staging and production. These environments were not identical, just mostly similar.

On top of all this, we used to do our local development and unit testing on Windows machines, while all other stages were run on Unix systems.

Working like this was not impossible, but it was a costly, time consuming effort to manage these environments with a lot of inherent risk that caused a lot of quality issues in all stages. Docker provides a solution to this problem.
