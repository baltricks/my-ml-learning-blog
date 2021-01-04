---
title: My first practice with an image classifier (using fastbook and fastai)
description: 
toc: true
layout: post
categories: [Image Classifier, fastbook, fastai]
comments: true

hide: false

---

# Which problem to solve
For my very first practice I followed the book I'm working with (*Deep Learning for Coders with fastai and PyTorch: AI Applications Without a PhD* by Jeremy Howard & Sylvain Gugger) and choose a bear image classifier as my first objective. 
Other ideas I had were image classifiers for birds or clouds.

# The input data
I used the DuckDuckGo search engine to find proper images in 3 categories as input data and stored them in the subfolders 'black', 'grizzly' and 'teddy'.
Then I created a new notebook with Google Colab (stored in Google Drive) and set the runtime to GPU. I copied my input data into a data folder in my drive and checked the input path with:
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
and set my path variable and got the images with
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
First a loaded my input data:
```python
bears = DataBlock(
    blocks=(ImageBlock, CategoryBlock), 
    get_items=get_image_files, 
    splitter=RandomSplitter(valid_pct=0.2, seed=42),
    get_y=parent_label,
    item_tfms=Resize(128))
dls = bears.dataloaders(path)
```


