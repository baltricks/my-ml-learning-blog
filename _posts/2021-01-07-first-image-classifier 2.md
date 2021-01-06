---
title: My first practice with an image classifier (using fastbook and fastai), Part II
description: Inference
toc: true
layout: post
categories: [Image Classifier, fastbook, fastai, Inference, Gui]
comments: true
image: /images/chap2Prediction-bear-black-small.PNG

hide: false

---

# Making predictions from the model
After exporting the model I wanted to make some predictions from the model. At first I did it in the training notebook on Google Colab to see how it works.
I checked the file with
```python
thisPath = Path()
thisPath.ls(file_exts='.pkl')
```
and built a new learner (the **inference** learner) from the model file:
```python
learn_inf = load_learner(thisPath/'export.pkl')
```
I made some single image predictions like
```python
learn_inf.predict(path + '/grizzly/' + '193_bear-1.jpg')
```
and got the categories of the model:
```python
learn_inf.dls.vocab
```
# Building a gui
The next step was to built a little gui - runnable in Jupyter Notebooks - to upload images and make predictions about their class (category).

Following the approach from the book (*Deep Learning for Coders with fastai and PyTorch: AI Applications Without a PhD* by Jeremy Howard & Sylvain Gugger) I could built this gui using the *IPython widgets*.

But I was still working within my training notebook on Google Colab. What I really wanted was a separate notebook without all this training stuff: just my self-trained model and some widgets and actions to get predictions from test images.

# Running on a local notebook
In the meantime I had installed Anaconda on my local computer and started some Python lessons within local Jupyter Notebooks (I am a coder but a Python newbie). So it was nearby to install the missing packages (fastai and PyTorch) and go on with my prediction gui on my local computer.

But I ran very soon into dependency issues. Finally this does the trick:
- I used the Anaconda Navigator to add a new environment and named it 'fastai'.
- I added the *fastai* and *pytorch* channels
- and installed the *pytorch*, *fastai* and *fastbook* packages

Now I can run notebooks using fastai in this environment [^1].

Then I copied all the neccesary code for inference from the training notebook and created a new local notebook for my gui.

And now the gui works. I can upload images and get the classification (also showing its probability)!

![]({{ site.baseurl }}/images/chap2Prediction-bear-black.PNG "Gui running in a notebook")




[^1]:there are still some issues with the gpu/cpu and the path (I'm working with Windows) - but I got it running.














