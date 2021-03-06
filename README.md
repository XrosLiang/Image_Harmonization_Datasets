<base target="_blank"/>

# Image_Harmonization_Datasets

**Image Harmonization** is to harmonize a composite image by adjusting its foreground appearances consistent with the background region. A real composite image is generated by a foreground region of one image combined with the background of another image. Though it's easy to create real composite images, the harmonized outputs are too time-consuming and skill-demanding to generate. So there is no high-quality publicly available dataset for image harmonization.

Our dataset is a synthesized dataset for Image Harmonization. It contains 4 sub-datasets: HCOCO, HAdobe5k, HFlickr, and Hday2night, each of which contains synthesized composite images, foreground masks of composite images and corresponding real images. The whole dataset is provided in  [**Baidu Cloud**](<https://pan.baidu.com/s/1DaepFq0l8XHiG8dhQr8EBw>) [**(Alternative_address)**](https://bcmi.cloud:5001/sharing/Kc3eFVFix)

| |HCOCO|HAdobe5k|HFlickr|Hday2night|
|:--:|:--:|:--:|:--:|:--:|
|Training set| 38545 |19437| 7449 |311|
|Test set| 4283 |2160| 828 |133|

- ### HCOCO

HCOCO, containing 42k synthesized composite images, is generated based on [Microsoft COCO](<http://cocodataset.org/>) dataset. The foreground region is corresponding object segmentation mask provided from COCO. Within the foreground region, the appearance of COCO image is edited using various color transfer methods. **The HCOCO sub-dataset and training/testing split are provided in [Baidu Cloud](https://pan.baidu.com/s/1bMTNzFJMreOOE-Lz3c7hGg)** [**(Alternative_address)**](https://bcmi.cloud:5001/sharing/KOBUL3QOs).


- ### HAdobe5k

HAdobe5k is generated based on [MIT-Adobe FiveK](<http://data.csail.mit.edu/graphics/fivek/>) dataset. Provided with 6 editions of the same image, we manually segment the foreground region and exchange foregrounds between 2 versions. **The HAdobe5k sub-dataset and training/testing split are provided in [Baidu Cloud](https://pan.baidu.com/s/1NAtLnCdY1-4uxRKB8REPQg)** [**(Alternative_address)**](https://bcmi.cloud:5001/sharing/xxpHXApjV).


- ### HFlickr

We collected 4833 images from [Flickr](<https://www.flickr.com/>). After manually segmenting the foreground region, we use the same method as HCOCO to generate HFlickr sub-dataset. **The HFlickr sub-dataset and training/testing split are provided in [Baidu Cloud](https://pan.baidu.com/s/1ZaCYo9Z21RGVgCwXgtvmbw)** [**(Alternative_address)**](https://bcmi.cloud:5001/sharing/SpeAHYMMT).




- ### Hday2night

Hday2night is generated based on [day2night](https://pan.baidu.com/s/1bCtVhhtb_EDool_UnN2Bjw) dataset. We manually segment the foreground region, which is cropped and overlaid on another image captured on a different time. **The Hday2night sub-dataset and training/testing split are provided in [Baidu Cloud](https://pan.baidu.com/s/1wTqGeB9SMweS5UAaxWof8A)** [**(Alternative_address)**](https://bcmi.cloud:5001/sharing/bQnyVoPwF).


![](examples/examples.jpg)

# Color Transfer Methods

To generate synthesized composite images, color transfer methods are adopted to transfer color information from reference images to real images. Considering that color transfer methods can be categorized into four groups based on parametric/non-parametric and correlated/decorrelated color space, we select one representative method from each group. Thanks to Wei Xu's efforts for releasing the code of color transfer method 1, 2 and 3 in their survey paper, we could implement color transfer methods specialized for foreground based on their implementation. And the source code of IDT regrain color transfer is downloaded from the author's [GitHub](https://github.com/frcs/colour-transfer)

### 1. global color transfer

--Parametric method in decorrelated color space. Implementation of paper *Color transfer between images* [[pdf]](https://www.cs.tau.ac.il/~turkel/imagepapers/ColorTransfer.pdf).

### 2. global color transfer in RGB color space

--Parametric method in correlated color space. Implementation of paper *Color transfer in correlated color space* [[pdf]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.530.2757&rep=rep1&type=pdf).

### 3. cumulative histogram mapping

--Non-parametric method in decorrelated color space. Implementation of paper  *Histogram-based prefiltering for luminance and chrominance compensation of multiview video* [[pdf]](https://ieeexplore.ieee.org/document/4539698).

### 4. IDT regrain color transfer

--Non-parametric method in correlated color space. Implementation of paper  *Automated colour grading using colour distribution transfer* [[pdf]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.458.7694&rep=rep1&type=pdf).

# Baselines

### Lalonde

J.-F. Lalonde et al. provides their implementation of ICCV 2007 paper:  Using color compatibility for assessing image realism in their [GitHub](https://github.com/jflalonde/colorRealism).

And we have arranged the code to a "click-and-run" way. 
`demo.m` is available in `/lalonde/colorStatistics/mycode/demo/`. 
Don't forget to specify the path of the code and results in your computer in `getPathName.m`, and run `setPath.m` before run `demo.m`to get everything ready.

### Xue

This is Xue's implementation of their paper in 2012 ACM Transactions on Graphics: Understanding and improving the realism of image composites 

`demo.m` is available in `/xue/demo/`. 

Notice to add the path of all dependent files using `addpath(genpath('../dependency'))`.



### Zhu

Jun-Yan Zhu released the code of their ICCV 2015 paper: Learning a discriminative model for the perception of realism in composite images in their [GitHub](<https://github.com/junyanz/RealismCNN>).

Notice that it requires matcaffe interface. We make some changes corresponds to our dataset including how to preprocess data and how to save the harmonized results. Don't forget to specify `DATA_DIR`,`MODEL_DIR` and `RST_DIR` before running `demo.m`.

The pre-trained models of Zhu's work can also be found in [BaiduCloud](https://pan.baidu.com/s/1_9UidT1rGNX0gYOYzjqITQ) and remember to put it under `MODEL_DIR`.

### DIH

This is a Tensorflow implementation based on the caffe network released by the original authors in their [GitHub](<https://github.com/wasidennis/DeepHarmonization>).

Besides, we also discard one inner-most convolutional layer and one inner-most deconvolutional layer to make it suitable for input of 256*256 size.

To train DIH, 

`python train.py --data_dir <Your Path to Dataset> --init_lr 0.0001 --batch_size 32`

Don't forget to specify the directory of Image Harmonization Dataset after `data_dir`.

Our trained model can be found in [BaiduCloud](https://pan.baidu.com/s/1GlUh660j0LMQaQ3iykaNJQ). To test and re-produce the results of DIH reported in our paper, run:

`python test.py`

### U-net

This code of CVPR 2017: Image-to-Image Translation with Conditional Adversarial Networks,  is released by Jun-Yan Zhu in their [GitHub](<https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix>)

Since our dataset is not organized like a normally aligned dataset, we have to implement image loading and processing part according to our dataset. For more details, you could refer to `data/ihd_dataset.py`. We implement the U-net backbone based on Zhu's implementation of unet_256, and train it alone instead of in an adversarial manner. Refer to `unet_model.py` for more details.

To train U-net:

`python train.py  --dataroot ./datasets/ihd/ --name unet --model unet --gpu_ids 1 --dataset_mode ihd --is_train 1 --no_flip --preprocess none --norm instance`

Our trained model can be found in [BaiduCloud](https://pan.baidu.com/s/1jcgP7Miwmfc-qqezWx8sgg).  Download and put it under `./unet/checkpoint/unet/` To test and re-produce the results of U-net reported in our paper, run:

`python test.py  --dataroot ./datasets/ihd/ --name unet --model unet --gpu_ids 1 --dataset_mode ihd --is_train 0 --no_flip --preprocess none --norm instance`

# Experiments

When conducting experiments, we merge training sets of four sub-datasets as a whole training set to train the model, and evaluate it on the test set of each sub-dataset and the whole test set. Here we show some example results of different baselines on our dataset.

![](examples/results_syn.jpg)

Besides, to evaluate the effectiveness of different methods in real scenarios, we also conduct user study on 99 real composite images, of which 48 images from Xue and 51 images from Tsai. Below we present several results of different baselines on real composite images. And 99 real composite images could be found in [BaiduCloud](https://pan.baidu.com/s/1z0fvp28gWswSCysw0eiUQg)

![](examples/results_real_comp.jpg)

# Bibtex

**When using images from our dataset, please cite our paper using the following BibTeX [[pdf](<https://arxiv.org/abs/1911.13239>)]:**



```
@inproceedings{dih2020,
title={Deep Image Harmonization via Domain Verification},
author={Wenyan Cong and Jianfu Zhang and Li Niu and Liu Liu and Zhixin Ling and Weiyuan Li and Liqing Zhang},
booktitle={CVPR},
year={2020}}
```

