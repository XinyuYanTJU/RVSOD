# RVSOD

===============================================================================

#### Designed by Zheng Wang,Xinyu Yan.

===============================================================================

The dataset can be downloaded from:

Google disk：https://drive.google.com/……

Baidu pan: https://pan.baidu.com/……

===============================================================================

### Files:
'videos': original videos(videoname.avi)

'img': original frames to be annotated(videoname_framenum.jpg)

'eye fixation data/mat': eye fixation annotations stored in mat files

'eye fixation data/img': eye fixation annotations in '.jpg' format

'manually annotated masks':manually annotated masks of salient object segmentation in '.png' format

'ranking saliency masks': masks of salient objects with gray values of 0 to 1 in '.png' and mat formats

===============================================================================
### Dataset splitting:
Training set: 185 videos,5336 labeled frames.

Validation set: 70 videos,2013 labeled frames. 

Testing set: 109 videos,3176 labeled frames.

===============================================================================

### Background:
  The datasets currently used for video saliency object detection are all these for video object segmentation. As a result, two problems have arisen.
  
  1.Insufficient quantity: The size of these datasets is not large enough, and there is a high degree of correlation between frames, which cannot meet the requirement for training a depth model.
  
  2.Inappropriate Ground-truth: On the one hand, the existing datasets only are dedicated to video segmentation, but not for detection of salient objects. Truly salient information cannot be learned from these datasets by the network. On the other hand, the motion attribute of objects detected from these videos cannot be considered as correct indicator for determining whether these objects are salient or not. In other word,moving objects in the video are not necessarily salient ones, vice verse.

===============================================================================
### Introduction
We have established a ranking saliency object dataset,called RVSOD (Ranking Video Salient Object Dataset) which marks the objects with the eye fixation points on the basis of the currently existing eye fixation datasets. The number of eye fixation points is used to determine the degree of saliency of each object, and different gray values are assigned to these objects according to associated degree of saliency. The more eye fixation points on the object, the more salientt we think the object is, and the closer the gray value of the object is to 1. The dataset contains more than 364 carefully selected video sequences. We labeled one frame in every five frames,and marked a total of 10K frame images. We removed video sequences that appear similar in the UCF and HOLLYWOOD2 datasets and these are not suitable for salient object detection (such as video sequences with close-ups of people or video sequences without subject objects).Our RVSOD contains video sequences with different number of object, object types, motion information, and scene complexity. To our best knowledge, this is the first large-scale dataset in the context of video saliency object detection. RVSOD introduces a new definition, ranking video saliency object detection, and provides a benchmark dataset for the field. In addition, the establishment of our dataset help address the problem of training data lacking for learning-based video saliency object detection as well.

===============================================================================
### Labeling process:
**1. Manually mark the salient objects according to the position of the eye fixation points.**

Manually mark the objects O1, O2, ... On in each frame of the image with eye fixation points.(such as the ones shown in Fig. 1(①))

**2. Assign different gray values to the salient objects according to the number of eye fixation points.**

According to the eye fixation points annotation files, the number of eye fixation points on each marked object in each frame image is calculated. The object with the highest number of eye fixation points is considered to be the most salient object, and the gray values of its pixels are set to 1.And the gray values of the pixels of the remaining objects are set according to the ratio of the number of eye fixation points to the number of eye fixation points of the most salient object.In this way, in each video frame, the gray values of the salient objects are distributed between 0 and 1.More eye fixation points placed on the object means higher degree of saliency.And the gray values of the pixels are closer to 1.Conversely,these gray values are near to 0.(such as the ones shown in Fig. 1(②))

