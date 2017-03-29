# Activity Recognition with RNN and Temporal-ConvNet
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[Chih-Yao Ma](http://shallowdown.wixsite.com/chih-yao-ma/me)\*, [Min-Hung Chen](https://www.linkedin.com/in/chensteven)\*

(\* equal contribution)

### This project will soon be largely revised and updated. Please stay tuned.

---
## Abstract
In this work, we demonstrate a strong baseline two-stream ConvNet using ResNet-101. We use this baseline to thoroughly examine the use of both RNNs and Temporal-ConvNets for extracting spatiotemporal information. Building upon our experimental results, we then propose and investigate two different networks to further integrate spatiotemporal information: 1) temporal segment RNN and 2) Inception-style Temporal-ConvNet.

Our analysis identifies spe- cific limitations for each method that could form the basis of future work. Our experimental results on UCF101 and HMDB51 datasets achieve state-of-the-art performances, 94.1% and 69.0%, respectively, without requiring extensive temporal augmentation.

---
#### How we tackle Activity Recognition problem?
<p align="center">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/overview_image.png?raw=true">
</p>

---
### Demo
The GIFs demonstrate the top-3 predictions results of our TS-LSTM and Temporal-Inception methods. The text on the top is the ground truth, three texts are the predictions for each of the method, and the bar right next to the predictions are how confident the model makes predictions.


<p align="center">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-1.gif?raw=true" width="250">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-2.gif?raw=true" width="250">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-3.gif?raw=true" width="250">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-4.gif?raw=true" width="250">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-5.gif?raw=true" width="250">
<img src="https://github.com/chihyaoma/Activity-Recognition-with-CNN-and-RNN/blob/master/figures/demo-6.gif?raw=true" width="250">
</p>

---
## Dataset
We are currently using [UCF101](http://crcv.ucf.edu/data/UCF101.php) and [HMDB51](http://serre-lab.clps.brown.edu/resource/hmdb-a-large-human-motion-database/) dataset for our project.


---
#### Prerequisites
* Linux (tested on Ubuntu 14.04)
* [Torch](http://torch.ch/docs/getting-started.html#_)
* [CUDA](https://developer.nvidia.com/cuda-downloads) and [cuDNN](https://developer.nvidia.com/cudnn)
* NVIDIA GPU is strongly recommended
* [torch-pastalog](https://github.com/Kaixhin/torch-pastalog) to visualize training status

---
## Usage
We proposed two different methods to train the models for activity recognition: TS-LSTM and Temporal-Inception.

#### Inputs
Our models takes the **feature vectors** generated by the first stage two-stream ConvNet as input for training. You can generate the features using our codes under "/CNN-Pred-Feat/". You can also download the feature vectors generated by us. (please refer to the Dropbox link below.) We followed the first training/testing split from [UCF-101](http://crcv.ucf.edu/data/UCF101.php). If you would like to compare with our results, please use the same training and testing list, as it will affect your overall performance a lot.

* Features for training:

|                 | UCF101          | HMDB51      |
|:-------------:|:-------------:|:---------:|
| RGB      | [sp1](https://www.dropbox.com/s/lxz10lijnh1gb6i/data_feat_train_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/0pqodpr7btj93m5/data_feat_train_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/nnljsen7xwxbfm1/data_feat_train_RGB_centerCrop_25f_sp3.t7?dl=0) | [sp1](https://www.dropbox.com/s/qvko5we5ccr16a3/data_feat_train_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/xna1c9travtgp7p/data_feat_train_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/nb5rpnc47rs6eia/data_feat_train_RGB_centerCrop_25f_sp3.t7?dl=0) |
| TV-L1       | [sp1](https://www.dropbox.com/s/fug14kobliewgb2/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/ju1v4bymtwbgrdp/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/343oko45z0xauz7/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)      |  [sp1](https://www.dropbox.com/s/nnzru9rkwaozw32/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/vk53sr16x3mo6pz/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/zt09zfnw2q97qop/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)  |



* Features for testing:

|                 | UCF101          | HMDB51      |
|:-------------:|:-------------:|:---------:|
| RGB      | [sp1](https://www.dropbox.com/s/x5slrzhos937bnv/data_feat_test_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/83hmoaezad8j8mj/data_feat_test_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/t0lqrehejzjomqu/data_feat_test_RGB_centerCrop_25f_sp3.t7?dl=0) | [sp1](https://www.dropbox.com/s/7vxs1n7id9x98jt/data_feat_test_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/x630x0x0mf1s1fx/data_feat_test_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/ot65vzgvz9f37dy/data_feat_test_RGB_centerCrop_25f_sp3.t7?dl=0) |
| TV-L1       | [sp1](https://www.dropbox.com/s/p48731hdg8m0fjo/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/9w0250idyysy99d/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/7xx5aqu0j79y4qt/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)      | [sp1](https://www.dropbox.com/s/zj4neexynd1lt0g/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/fvfp1943ctuq6ya/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/egfwm4rbdqay46q/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)   |


#### Train with RNN
We use the [RNN library](https://github.com/Element-Research/rnn) provided by Element-Research. Simply install it by:
```bash
$ luarocks install rnn
```
After you downloaded the feature vectors, please modify the code in *./RNN/data-ucf101.lua* to the director where you put your feature vector files.

To start the training process, go to *./RNN* and simply execute:
```bash
$ th main.lua -pastalogName 'model_RNN' -nGPU 1 -dataset 'ucf101' -split '1' -fcSize '{0}' -hiddenSize '{512}' -lstm -spatFeatDir '<path/to/feature/>' -tempFeatDir '<path/to/feature/>'
```
The training and testing loss will be reported, and the results will be saved into log files. The learning rate and best testing accuracy will be reported each epoch if there is any update.

#### Train with Temporal-ConvNet
To start the training process, go to *./TCNN* and simply execute:
```bash
$ qlua run.lua -r 15e-5
```
For more details, please refer to the readme file in the folder *./TCNN/*.

You also need to modify the code in *./TCNN/data.lua* to the director where you put your feature vector files.

The training and testing performance will be plotted, and the results will be saved into log files. The best testing accuracy will be reported each epoch if there is any update.

---
## Acknowledgment
This work was initialized as a class project for deep learning class in Georgia Tech 2016 Spring. We were teamed up with Hao Yan and Casey Battaglino to work on this class project, who have been a great help and provide valuable discussions as we go long this class project.

#### Please contact us if you have any questions.

[Chih-Yao Ma](http://shallowdown.wix.com/chih-yao-ma/me) at <cyma@gatech.edu> or [[LinkedIn]](https://www.linkedin.com/in/chih-yao-ma-9b5b3063)

[Min-Hung Chen](https://www.linkedin.com/in/chensteven) at <cmhungsteve@gatech.edu>
