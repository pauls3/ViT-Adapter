# HTC++

> [Improved Hybrid Task Cascade by Swin Paper](https://arxiv.org/abs/2103.14030)

<!-- [ALGORITHM] -->

## Abstract

For system-level comparison, Swin adopts an improved HTC (denoted as HTC++) with instaboost, stronger multi-scale training (resizing the input such that the shorter side is between 400 and 1400 while the longer side is at most 1600), 6x schedule (72 epochs with the learning rate decayed at epochs 63 and 69 by a factor of 0.1), softNMS, and an extra global self-attention layer appended at the output of last stage and ImageNet-22K pre-trained model as initialization.

## Introduction

HTC++ requires COCO and [COCO-stuff](http://calvin.inf.ed.ac.uk/wp-content/uploads/data/cocostuffdataset/stuffthingmaps_trainval2017.zip) dataset for training. You need to download and extract it in the COCO dataset path.
The directory should be like this.

```none
detection
├── configs
├── data
│   ├── coco
│   │   ├── annotations
│   │   ├── train2017
│   │   ├── val2017
│   │   ├── test2017
|   |   ├── stuffthingmaps
```

## Results and Models

The results on COCO mini-val and test-dev are shown in the below table.

<table>
   <tr  align=center>
      <td rowspan="2" align=center><b>Backbone</b></td>
      <td rowspan="2" align=center><b>Pre-train</b></td>
      <td rowspan="2" align=center><b>Lr schd</b></td>
      <td colspan="2" align=center><b>mini-val</b></td>
      <td colspan="2" align=center><b>test-dev</b></td>
      <td rowspan="2" align=center><b>#Param</b></td>
      <td rowspan="2" align=center><b>Config</b></td>
      <td rowspan="2" align=center><b>Download</b></td>
   </tr>
   <tr>
      <td>box AP</td>
      <td>mask AP</td>
      <td>box AP</td>
      <td>mask AP</td>
   </tr>
   <tr align=center>
      <td>ViT-Adapter-L</td>
      <td><a href="https://conversationhub.blob.core.windows.net/beit-share-public/beit/beit_large_patch16_224_pt22k_ft22k.pth">BEiT-L</a></td>
      <td>3x</td>
      <td>58.4</td>
      <td>50.8</td>
      <td><a href="https://drive.google.com/file/d/1lXQxf5PJ0g0bQNkMMrhG63jal0NsmYjb/view?usp=sharing">58.9</a></td>
      <td><a href="https://drive.google.com/file/d/1nyuONJcHHXki0Cn8dCgbPZ9D_MURh47t/view?usp=sharing">51.3</a></td>
      <td>401M</td>
      <td><a href="./htc++_beit_adapter_large_fpn_3x_coco.py">config</a> </td>
      <td><a href="https://github.com/czczup/ViT-Adapter/releases/download/0.3.0/htc++_beit_adapter_large_fpn_3x_coco.pth.tar">model</a> | 
        <a href="https://github.com/czczup/ViT-Adapter/releases/download/0.3.0/20220604_210212.log">log</a></td>
   </tr>
   </tr>
   <tr align=center>
      <td>ViT-Adapter-L (MS)</td>
      <td><a href="https://conversationhub.blob.core.windows.net/beit-share-public/beit/beit_large_patch16_224_pt22k_ft22k.pth">BEiT-L</a></td>
      <td>3x</td>
      <td>60.2</td>
      <td>52.2</td>
      <td><a href="https://drive.google.com/file/d/15t2Oc3FiNeLr6RnKOJ-0IbI7b2LalxbX/view?usp=sharing">60.4</a></td>
      <td><a href="https://drive.google.com/file/d/1TIPOJC6ieZS_ZRNCbo_AW4UqYAkQIjyN/view?usp=sharing">52.5</a></td>
      <td>401M</td>
      <td>-</td>
      <td>-</td>
   </tr>
</table>

- MS denotes multi-scale testing. Note that the ms config is only for testing.
- We use 16 A100 GPUs with 1 image/GPU for ViT-Adapter-L models.

## Old Results

The results on COCO mini-val and test-dev are shown in the below table.

<table>
   <tr align=center>
      <td rowspan="2" align=center><b>Backbone</b></td>
      <td rowspan="2" align=center><b>Pre-train</b></td>
      <td rowspan="2" align=center><b>Lr schd</b></td>
      <td colspan="2" align=center><b>mini-val</b></td>
      <td colspan="2" align=center><b>test-dev</b></td>
      <td rowspan="2" align=center><b>#Param</b></td>
      <td rowspan="2" align=center><b>Config</b></td>
      <td rowspan="2" align=center><b>Download</b></td>
   </tr>
   <tr>
      <td>box AP</td>
      <td>mask AP</td>
      <td>box AP</td>
      <td>mask AP</td>
   </tr>
   <tr align=center>
      <td>ViT-Adapter-L</td>
      <td><a href="https://conversationhub.blob.core.windows.net/beit-share-public/beit/beit_large_patch16_224_pt22k_ft22k.pth">BEiT-L</a></td>
      <td>3x</td>
      <td>57.9</td>
      <td>50.2</td>
      <td><a href="https://drive.google.com/file/d/11zpPSvmuAn7aP5brxzHE8naObnOfFxby/view?usp=sharing">58.5</a></td>
      <td><a href="https://drive.google.com/file/d/1wIbtzfHfPqkvZaSivzcsh4HWu1oSiun6/view?usp=sharing">50.8</a></td>
      <td>401M</td>
      <td><a href="./htc++_beit_adapter_large_fpn_3x_coco_old.py">config</a> </td>
      <td><a href="https://github.com/czczup/ViT-Adapter/releases/download/v0.1.0/htc++_beit_adapter_large_fpn_3x_coco_old.pth.tar">model</a> | 
        <a href="https://github.com/czczup/ViT-Adapter/releases/download/v0.1.0/20220512_030903.log">log</a></td>
   </tr>
   </tr>
   <tr align=center>
      <td>ViT-Adapter-L (MS)</td>
      <td><a href="https://conversationhub.blob.core.windows.net/beit-share-public/beit/beit_large_patch16_224_pt22k_ft22k.pth">BEiT-L</a></td>
      <td>3x</td>
      <td>59.8</td>
      <td>51.7</td>
      <td><a href="https://drive.google.com/file/d/1i-qjgUK4CMwZcmu5pkndldwfVbdkw5sU/view?usp=sharing">60.1</a></td>
      <td><a href="https://drive.google.com/file/d/16mlEOPY7K-Xpx_CL650A-LWbVDm2vl4X/view?usp=sharing">52.1</a></td>
      <td>401M</td>
      <td>-</td>
      <td>-</td>
   </tr>
</table>

- MS denotes multi-scale testing. Note that the ms config is only for testing.
- We use 16 A100 GPUs with 1 image/GPU for ViT-Adapter-L models.
