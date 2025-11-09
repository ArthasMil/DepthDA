# Exploiting Relative Depth for Cross-domain Semantic Segmentation of High-resolution Satellite Remote Sensing Images

## Introduction
Official codebase of the paper **Exploiting Relative Depth for Cross-domain Semantic Segmentation of High-resolution Satellite Remote Sensing Images** by ***Yongqi Sun, Chenguang Dai, Yu Su, Yujun Quan, Zhenchao Zhang, Meilin Li and Anzhu Yu***.

In this manuscript, we proposed a novel framework for improving the generalization ability of the **cross-domain remote sensing image semantic segmentation** problem by integrating the relative depth (rDepth) maps derived from Depth Anything Model.

The framework encodes rDepth into the network, fuses it with optical image feature maps, and achieves pixel-wise segmentation through multi-scale fusion and decoding. Experiments on public and self-built datasets show that integrating rDepth significantly improves cross-domain performance, even approaching state-of-the-art (SOTA) UDA accuracy in some cases.


## Main Results

We use two remote sensing datasets for an evaluation of the proposed framework: The LoveDA dataset and a self-constructed dataset (release in the future).

We used the LoveDA dataset one domain train split for model training and predicting the semantic masks of the test set from another domain. Here is the main results of the **Urban to Rural**:

| RGB backbone       | rDepth backbone | Type  | Background | Building | Road   | Water  | Barren | Forest | Agriculture | mIoU  |
|--------------------|-----------------|-------|------------|----------|--------|--------|--------|--------|-------------|-------|
| TransNorm          | -               | AT    | 19.39      | 36.30    | 22.04  | 36.68  | 14.00  | 40.62  | 3.30        | 24.62 |
| FADA               | -               | AT    | 24.39      | 32.97    | 25.61  | 47.59  | 15.34  | 34.35  | 20.29       | 28.65 |
| CLAN               | -               | AT    | 22.93      | 44.78    | 25.99  | 46.81  | 10.54  | 37.21  | 24.45       | 30.39 |
| PyCDA              | -               | ST    | 12.36      | 38.11    | 20.45  | 57.16  | 18.32  | 41.90  | 32.14       | 32.14 |
| AdaptSegNet        | -               | AT    | 26.89      | 40.53    | 30.65  | 50.09  | 16.97  | 32.51  | 28.25       | 32.27 |
| DeeplabV3          | -               | -     | 26.64      | 48.14    | 23.37  | 43.97  | 11.35  | 32.47  | 50.61       | 33.79 |
| CBST               | -               | ST    | 25.06      | 44.02    | 23.79  | 50.48  | 8.33   | 39.16  | 49.65       | 34.36 |
| IAST               | -               | ST    | 29.97      | 49.48    | 28.29  | 64.49  | 2.13   | 33.36  | 61.37       | 38.44 |
| SegFormer          | -               | -     | 26.60      | 55.80    | 35.62  | 65.44  | 17.13  | 40.13  | 39.65       | 40.05 |
| DCA                | -               | ST    | 36.38      | 55.89    | 40.46  | 62.03  | 22.01  | 38.92  | 60.52       | 45.17 |
| ST-DASegNet (DeeplabV3) | -        | AT+ST | 36.78      | 59.83    | 39.69  | 69.28  | 14.19  | 44.79  | 62.16       | 45.69 |
| ST-DASegNet (SegFormer) | -        | AT+ST | 37.39      | 52.84    | 41.99  | 72.05  | 11.46  | 46.79  | 61.27       | 46.25 |
| ST-DASegNet (SegFormer) | -        | AT+ST | 36.78      | 59.83    | 43.77  | 73.83  | 19.38  | 49.96  | 67.01       | 50.08 |
| ConvNeXt-B (Baseline) | -          | -     | 35.51      | 56.14    | 40.88  | 70.05  | 13.99  | 48.42  | 64.91       | 47.13 |
| **ConvNeXt-B**(ours)         | **ConvNeXt-S** (ours)    | -     | 36.79      | 59.27    | 46.97  | 71.31  | 19.87  | 41.62  | 67.05       | **48.98** |
| **ConvNeXt-XL**(ours)      | **ConvNeXt-B**   (ours)   | -     | 37.23      | 63.05    | 42.69  | 71.71  | 19.91  | 45.03  | 68.36       | **49.71** |

**Rural to Urban**:
| RGB backbone               | rDepth backbone | Type  | Background | Building | Road   | Water  | Barren | Forest | Agriculture | mIoU  |
|----------------------------|-----------------|-------|------------|----------|--------|--------|--------|--------|-------------|-------|
| TransNorm                  | -               | AT    | 38.37      | 5.04     | 3.75   | 80.83  | 14.19  | 33.99  | 17.91       | 27.73 |
| FADA                       | -               | AT    | 43.89      | 12.62    | 12.76  | 80.37  | 12.70  | 32.76  | 24.79       | 31.41 |
| AdaptSegNet                | -               | AT    | 42.35      | 23.73    | 15.61  | 81.95  | 13.62  | 28.70  | 22.05       | 32.68 |
| CLAN                       | -               | AT    | 43.41      | 25.42    | 13.75  | 79.25  | 13.71  | 30.44  | 25.80       | 33.11 |
| DeeplabV3                  | -               | -     | 32.81      | 43.41    | 27.59  | 79.23  | 14.84  | 29.24  | 20.97       | 35.44 |
| PyCDA                      | -               | ST    | 38.04      | 35.86    | 45.51  | 74.87  | 7.71   | 40.39  | 11.39       | 36.25 |
| IAST                       | -               | ST    | 48.57      | 31.51    | 28.73  | 86.01  | 20.29  | 31.77  | 36.50       | 40.48 |
| SegFormer                  | -               | -     | 44.98      | 43.93    | 27.46  | 85.82  | 16.24  | 37.02  | 30.48       | 40.85 |
| CBST                       | -               | ST    | 48.37      | 46.10    | 35.79  | 80.05  | 19.18  | 29.69  | 30.05       | 41.32 |
| ST-DASegNet (DeepLabV3)    | -               | AT+ST | 49.68      | 51.62    | 52.41  | 74.76  | 10.69  | 35.67  | 35.79       | 44.38 |
| DCA                        | -               | ST    | 45.82      | 49.60    | 51.65  | 80.88  | 16.70  | 42.93  | 36.92       | 46.36 |
| DAFormer                   | -               | ST    | 50.94      | 56.66    | 62.83  | 89.41  | 11.99  | 45.81  | 25.26       | 48.99 |
| ST-DASegNet (SegFormer)    | -               | AT+ST | 51.01      | 54.23    | 60.52  | 87.31  | 15.18  | 47.23  | 36.26       | 50.28 |
| ConvNeXt-B (Baseline)      | -               | -     | 46.77      | 46.52    | 37.27  | 82.30  | 17.33  | 42.34  | 36.27       | 44.11 |
| ConvNeXt-B                 | ConvNeXt-B      | -     | 48.23      | 52.68    | 42.70  | 77.18  | 16.62  | 40.85  | 48.86       | 46.73 |
| ConvNeXt-XL                | ConvNeXt-B      | -     | 50.56      | 51.81    | 42.89  | 85.11  | 16.69  | 42.67  | 44.00       | 47.68 |


More results could be found at  [<b>LoveDA Unsupervised Domain Adaptation Challenge</b>](https://codalab.lisn.upsaclay.fr/competitions/424) 

We introduced some data augmentation tricks and now ranked *5th* in *Urban to Rural Competition*, which outperformed many *UDA approaches* using fully supervised learning approach.

<div align="center">
  <img src="https://github.com/ArthasMil/DepthDA/blob/main/leaderboard_u2r.png?raw=true">
</div>

## Code 

Implemented with MMsegmenataion.

Available when the paper accepted. 
