---
title: When my ML learning starts
description: An exciting book - My coding environment -  What I've learned until now
toc: false
layout: post
categories: [fastai, Google Colab]
comments: true
---

# An exciting book

In late 2020 I came across *Deep Learning for Coders with fastai and PyTorch: AI Applications Without a PhD* by Jeremy Howard & Sylvain Gugger and I was directly inspired and excited to dive into deep learning. Deep Learning, Machine Learning, AI and all the other terms of artifical intelligence had been very unclear to me - even though I'd been working for many years as a software developer. But with this book I got the feeling that the door to this domain is now opened to me - by authors with long lasting experience in coding and teaching AI. 

# My coding environment

Following the book coding should take place in Jupyter Notebooks. After looking around for the different ways to get own Jupyter Notebooks running I decided to start with Google Colab for my notebooks. Although there are some issues to keep in mind:

1. Colab Notebooks differ from the typical Jupyiter Notebook GUI
2. Google doesn't garantee access to GPUs (which is highly recommended when training your models). So you can run temporarily into performance issues.
3. The Colab platform doesn't support Voila, which will be used for publishing purposes

From the [books website](https://course.fast.ai/) you can start any of the books chapters (the book itself is written in Jupyter Notebooks). From there you can copy or create new notebooks and store them in Google Drive. The only prerequisite is a Google Account. That's all.

That's the way I started creating and running my very first notebooks. Then I rebuilt the first prepared samples (image classifier and others) coming with the book.

# What I've learned until now

Each chapter of the book ends with a questionnaire which helps you checking your learning progress. 

I enjoy it. It's very useful.

Some of the main topics I took from the first chapter:

- the main areas of deep learning
- from the first artificial neurons to **neuronal networks**
- running the first notebook
- **machine learning** as another way (other than writing a program) to let computers do their task - by learning from their experience (= **training**)
- a first idea how training works
- **predictions** coming from input data
- different types of models like **classification** and **regression**
- the meaning of input data and its division into different data sets like a **training set** used as training input, **validation set** (or development set) to measure the accuracy of a model and optional a separate **test set** to test a model with never seen data
- jargon: **architecture**, **parameters**, **labels**, **epoch**, **metric**, **loss**, **overfitting**, **hyperparameters**, ...
- a first use of a convolutional neural network (**CNN**)
- the use of **pretrained models** (and **fine-tuning**)
- image recognition can be used for non-image tasks (for example spectograms for sound issues)

