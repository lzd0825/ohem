This directory holds (*after you download them*):
- Fast R-CNN models trained with OHEM on VOC 2007 trainval
- Caffe models pre-trained on ImageNet
- Symlinks to datasets

To download Fast R-CNN models (VGG_CNN_M_1024, VGG16) trained with OHEM on VOC 2007 trainval, run:

```
./data/scripts/fetch_fast_rcnn_ohem_models.sh
```

This script will populate `data/fast_rcnn_ohem_models` with VGG16 and VGG_CNN_M_1024 models (Fast R-CNN detectors trained with OHEM).


To download Caffe models (ZF, VGG16) pre-trained on ImageNet, run:

```
./data/scripts/fetch_imagenet_models.sh
```

This script will populate `data/imagenet_models`.

In order to train and test with PASCAL VOC, you will need to establish symlinks.
From the `data` directory (`cd data`):

```
# For VOC 2007
ln -s /your/path/to/VOC2007/VOCdevkit VOCdevkit2007

# For VOC 2012
ln -s /your/path/to/VOC2012/VOCdevkit VOCdevkit2012
```

Install the MS COCO dataset at /path/to/coco

```
ln -s /path/to/coco coco
```

For COCO with Fast R-CNN, place object proposals under `coco_proposals` (inside
the `data` directory). You can obtain proposals on COCO from Jan Hosang at
https://www.mpi-inf.mpg.de/departments/computer-vision-and-multimodal-computing/research/object-recognition-and-scene-understanding/how-good-are-detection-proposals-really/.
For COCO, using MCG is recommended over selective search. MCG boxes can be downloaded
from http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/mcg/.
Use the tool `lib/datasets/tools/mcg_munge.py` to convert the downloaded MCG data
into the same file layout as those from Jan Hosang.

Since you'll likely be experimenting with multiple installs of Fast/er R-CNN in
parallel, you'll probably want to keep all of this data in a shared place and
use symlinks. On my system I create the following symlinks inside `data`:

Annotations for the 5k image 'minival' subset of COCO val2014 that I like to use
can be found at http://www.cs.berkeley.edu/~rbg/faster-rcnn-data/instances_minival2014.json.zip.
Annotations for COCO val2014 (set) minus minival (~35k images) can be found at
http://www.cs.berkeley.edu/~rbg/faster-rcnn-data/instances_valminusminival2014.json.zip.

```
# data/cache holds various outputs created by the datasets package
ln -s /data/fast_rcnn_shared/cache

# move the imagenet_models to shared location and symlink to them
ln -s /data/fast_rcnn_shared/imagenet_models

# move the selective search data to a shared location and symlink to them
# (only applicable to Fast R-CNN training)
ln -s /data/fast_rcnn_shared/selective_search_data

ln -s /data/VOC2007/VOCdevkit VOCdevkit2007
ln -s /data/VOC2012/VOCdevkit VOCdevkit2012
```
