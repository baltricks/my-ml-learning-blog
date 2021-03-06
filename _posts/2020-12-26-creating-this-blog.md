---
title: Creating this blog
description: Why do I write this blog? - A GitHub Page for my blog - Changing to fastpages
toc: false
layout: post
categories: [GitHub Page]
comments: true

---

# Why do I write this blog?

One really good reason to write this blog is: it **improves my understanding** of what I'm doing and learning!

But there is more:

As a developer I often feel how important it is for me
- to stay focused on my (or my companies) goals
- to frequently recap what I've done or learned and how succesful it was
- to see and remember the progress and not only what's missing
- and to keep the balance between diving deeply into things on one side and reacting to upcoming needs on the other side

So a great part of this work is just thinking and making decisions. And that's another reason to write this blog: **It should help me to keep myself on this road**.

And another important reason is my hope that this blog will **one day help others on their way**. Sharing content makes learning and development available for everybody. I benefit from this since years. 

# A GitHub Page for my blog

{% include alert.html text="This text references a previous version of this blog created with GithHub Pages. It's still <a target=\"_blank\" href=\"https://baltricks.github.io/my-ml-page/\">online here</a> for demonstration purposes only" %}

To keep things easy I decided to use [GitHub Pages](https://pages.github.com) for this blog. I created a new git repository on GitHub and choose the main branch as page source and the [cayman theme](https://github.com/pages-themes/cayman) as Jekyll theme. All this can be done in the *Settings / Github Pages* section of the repository.

In this repository I created a directory structure for my future posts and made my adaptations in the *index.md* (as the home page of the blog) and *_config.yml* (the theme configuration). For layout customization I copied the *_layouts/default.html* from the [origin theme repository](https://github.com/pages-themes/cayman) into my repository and made my (minor) changes.

So I could create my first post (*\*.md*) and reference it in my home page of the blog (*index.md*). The posts are written in the markdown syntax of the GitHub platform. You can find a short markdown guide [here](https://guides.github.com/features/mastering-markdown/).

When I began to fill my first post with content I changed the process. Previously I did all editing via browser in the GitHub web site. But then I changed to my local computer: I used my *Git Bash* (I'm working on Windows) to clone the repository and made my editing locally with *Visual Studio Code*. There is a very nice extension called *Markdown All in One* which helps you writing pages in the markdown syntax. Now - when ready for publishing - I only have to push my content to the origin repository. The page updates automatically.

# Changing to fastpages

Some days later when I had built my first model I began thinking about publishing also code or models. I made some experience with [Binder](https://mybinder.org/) and learned how to start a *jupyter notebook* with *Binder* (*Binder* lets you run *docker images* built from *jupyter notebooks*). Here is a simple example (don't worry, it may take some moments when (re)building and launching the image):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/baltricks/my-ml-learning-blog/HEAD?filepath=others%2Fsay-hello-world.ipynb)

And finally I read about [fastpage](https://github.com/fastai/fastpages), a platform that brings blogging and running *jupyter notebooks* together: It supports *jupyter notebooks* as blog posts! **So you can write a blog post together with runnable code in a *jupyter notebook* and integrate a button to start the post / notebook itself on a platform like Binder!**

These were the main steps I took to migrate my blog to *fastpage*:

- First I followed the [instructions](https://github.com/fastai/fastpages#setup-instructions) to setup my new page
- I customized the page in:
  - _config.yml (social links, title, description, show_image)
  - _pages/about.md (about me)
  - index.html
  - _includes/footer.html (copied from the origin minima theme, removed the RSS subscription link)
- Migrating my posts:
  - copied my former posts into the _posts folder of the new page
  - changed the names according to the naming convention
  - added following tags:
    - toc: true / false
    - layout: post
    - categories: [...] 
    - optional image
  - removed the initial posts
- Enabled comments for github users:
  - enabled the utterances app https://github.com/apps/utterances (see instructions [here](https://github.com/fastai/fastpages#enabling-comments))
  - set 'coments: true' for all posts

So my page gots also the following features coming with *fastpage*:

- a search page
- a tags page showing the contents and categories 
- pagination in the index page
- comments enabled in my posts

