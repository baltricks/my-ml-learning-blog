---
title: My first practice with an image classifier (using fastbook and fastai), Part I
description: Which problem to solve until Finishing the training
toc: true
layout: post
categories: [Image Classifier, fastbook, fastai, Google Colab, Training]
comments: true
image: /images/chap2BearsFineTune.PNG

hide: false

---

# Which problem to solve
For my very first practice I followed the book (*Deep Learning for Coders with fastai and PyTorch: AI Applications Without a PhD* by Jeremy Howard & Sylvain Gugger) and choose the **bear image classifier** as my first objective. 

# Starting with the input data and Google Colab
I used the DuckDuckGo search engine to find proper images in 3 categories as input data and stored them in the subfolders 'black', 'grizzly' and 'teddy'.
Then I created a new notebook with Google Colab (stored in Google Drive) and set the runtime to GPU. I copied my input data into a data folder on my drive and checked the input path with:
```python
!ls drive/MyDrive/data/images/bears
```
and after installing and setting up fastbook
```python
!pip install -Uqq fastbook
import fastbook
fastbook.setup_book()
```
I also checked the mounted drive
```python
!ls gdrive/MyDrive/data/images/bears 
```
Before continuing let me show the imports I finally needed in my training notebook:
```python
from fastbook import get_image_files, verify_images, Path, DataBlock, ImageBlock, CategoryBlock
from fastbook import RandomSplitter, parent_label, Resize, ResizeMethod, RandomResizedCrop, aug_transforms
from fastbook import cnn_learner, resnet18, error_rate, load_learner
from fastbook import ClassificationInterpretation
from fastai.vision.widgets import ImageClassifierCleaner, widgets, PILImage, VBox
```

Next step was to set my path variable and get the images
```python
path = 'gdrive/MyDrive/data/images/bears'
fns = get_image_files(path)
```
After verifying the images and unlinking the failed ones 
```python
failed = verify_images(fns)
failed.map(Path.unlink)
```
there were 495 images (in 3 categories) left.

# Training a model
First I made some specifications about the input data of the training process:
```python
bears = DataBlock(
    blocks=(ImageBlock, CategoryBlock), 
    get_items=get_image_files, 
    splitter=RandomSplitter(valid_pct=0.2, seed=42),
    get_y=parent_label,
    item_tfms=Resize(128))
```
This means that
- predictions should be made from images (the independent variable) to categories (the dependent variable)
- the items should be taken by the *get_image_files* function (which is taking a path as argument)
- the data set should be splitted randomly into a training and validation set (20% of the data for the validation set; randomly, but always the same sets)
- the labeling of the dependent variable (the categories, the y-value) should come from the folder name
- and all items (images) should be transformed - here resized - to the same size of 128px

Then I set the input path and got the data loaders:
```python
dls = bears.dataloaders(path)
```

Before starting the training I played around with some transformations available for 
- images (resizing with different methods) and
- batches of images (random image variations, the data augmentation)
and watched the results printed with the *show_batch* function of the dataloaders (*dls.train* for the training set and *dls.valid* for the validation set).

Then I followed the recommendation and made this settings:
```python
bears = bears.new(
    item_tfms=RandomResizedCrop(224, min_scale=0.5),
    batch_tfms=aug_transforms())
dls = bears.dataloaders(path)
```

I created the learner:
```python
learn = cnn_learner(dls, resnet18, metrics=error_rate)
```
using:
- a convolutional neural network (CNN)
- the data loaders defined before
- the *resnet18* as model architecture
- the *error rate* as the metric for the quality (that's the error rate of the predictions made with the validation set)
- a **pretrained model** (by default)

and started the **fine tuning** of the pretrained model with 4 epochs:
```python
learn.fine_tune(4)
```

The next step was looking at the result and making some **data cleaning**. Therefor I used the *ClassificationInterpretation* from fastbook (to plot the *confusion matrix* and see the top losses) and the *ImageClassifierCleaner* from fastai to define which images should be deleted or moved to another category:
```python
cleaner = ImageClassifierCleaner(learn)
cleaner
```

Deleting or moving can then be done with:
```python
for idx in cleaner.delete(): cleaner.fns[idx].unlink()
for idx,cat in cleaner.change(): shutil.move(str(cleaner.fns[idx]), path/cat)
```

# Finishing the training
I repeated fine tuning and data cleaning until I got this result from fine tuning (which came with the 3. or 4. run):

![]({{ site.baseurl }}/images/chap2BearsFineTune.PNG "Result from fine tuning")

Then I saved the model (**architecture** and **parameters**) with the export function of the learner:
```python
learn.export()
```
which creates the model file *export.pkl* (this file even includes information about the dataloaders). I downloaded and renamed it for local use.









