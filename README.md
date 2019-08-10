# Image_Harmonization_Datasets

This dataset is a synthesized dataset for **Image Harmonization**. It contains 4 sub-datasets: HCOCO, HAdobe5k, HFlickr and Hday2night, each of which contains synthesized composite images, foreground masks of composite images and corresponding real images. 



| |HCOCO|HAdobe5k|HFlickr|Hday2night|
|:--:|:--:|:--:|:--:|:--:|
|Traning set| |[3896](https://pan.baidu.com/s/1fBr5EdAGP9iZULyF9GDt1w)| |[429](https://pan.baidu.com/s/1yp60iqZRB98-csieLN_nug)|
|Test set| |[433](https://pan.baidu.com/s/1n92lEn45MTxObcZeXAxKRg)| |[48](https://pan.baidu.com/s/127E0T594rMQZ0OIyTL3vXA)|

- ### HCOCO

[HCOCO](https://pan.baidu.com/s/1cjDBYWZYiqKgFNPL62LLEg) , containing 50k synthesized composite images, is generated based on **Microsoft COCO** dataset. The foreground region is corresponding object segmentation mask provided from COCO. Within foreground region, the appearance of COCO image is edited using various color transfer methods.

- ### HAdobe5k

[HAdobe5k](https://pan.baidu.com/s/1EnaKSLfr_CTn6CbyQeEyMg) is generated based on **MIT-Adobe FiveK** dataset. Provided with 6 editions of the same image, we manually segment the foreground region and exchange foregrounds between 2 editions.

- ### HFlickr

We collected 5460 images from **Flickr**. After manually segmenting the foreground region, we use the same method as HCOCO to generate [HFlickr](https://pan.baidu.com/s/1EMUBmQWwQbUEOfFMIPsRxg) sub-dataset.

- ### Hday2night

[Hday2night](https://pan.baidu.com/s/1ia_P3-cmjwbpsfszntbTmQ) is generated based on **day2night** dataset. We manually segment the foreground region, which is cropped and overlaid on another image captured on different time.


