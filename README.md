<style>
.row {
  display: flex;
}

/* Create three equal columns that sits next to each other */
.column {
  flex: 33.33%;
  padding: 5px;
} 
}
</style>

## Problem Statement and Introduction

Food classification is the focus of our study and we have used 3 datasets to catogorize food dishes into different classes. First dataset consists of various food groups such as rice, breads, milk etc. Second one classifies them based on various regions of the world. Third dataset has 101 classes comprising a variety of foods. Food categories are too broad especially when it deals with multi cuisine dishes. Other challenge is to make model learn from different type of images under same class. We have proposed different models to train the model and classify the images in desired classes. The another challenge we faced is imbalanced classes in dataset, for which we have tried many methods which are explained in this report. Problem statement is to train model to do classification of food and study the impact of different training setup in food classification application by interchanging different CNN models like ResNet18, DenseNet121 & MobileNetV2 and hyper parameters like learning rate, no of epochs, no of fc layer, batch size, activation function, dropouts, normalization, image transformation, optimizers, etc on 3 different datasets: Food101, Food11k & World-Cuisines

## Data Description

| Name | Number of Images | | Classes | 
| ------ | ------ | ------ | ------ |
| Food 101 | 4000 | | 4 |
| World Cusine | 13800 | | 6 |
| Food-11k | 16643 | | 11 |

## Model Description
| Name | n_params | acc@1 |  acc@5 | Link | 
| ------ | ------ | ------ | ------ | ------ |
| Mobilenetv2 | 3504872 | 71.878 | 90.286 | [Link](https://arxiv.org/abs/1801.04381) |
| Densenet121 | 7978856 | 	74.434 | 91.972 | [Link](https://arxiv.org/abs/1608.06993) |
| Resnet18 | 11689512 | 69.758 | 89.078 | [Link](https://arxiv.org/pdf/1512.03385.pdf) |

***acc** measured on IMAGENET-1K dataset





## Hyperparameter Optimization

 - **Grid Search**
	The simplest approach for hyperparameter optimization is grid search. We essentially create a discrete grid from the domain of hyperparameter space. Each point, consisting of several hyperparameters, in the grid is used to evaluate the model. The grid's ideal set of values for the hyperparameters is where we get optimal results. This method is exhaustive and computationally expensive for Deep-Learning algorithms. The grid also grows exponentially as more dimensions are added. This makes it impractical to use when the number of hyperparameters is large.
	 
 - **Random Search**
	 We randomly sample some points from the domain in a random search and test the model's performance. Instead of searching exhaustively through the grid, we can define the number of experiments we want to carry out and then randomly sample hyperparameters values from each experiment from the search space. It is computationally cheaper than the grid search.

![enter image description here](https://miro.medium.com/max/828/1*9W1MrRkHi0YFmBoHi9Y2Ow.webp)*Grid Search vs Random Search*

**Our Approach**
We used random search for hyperparameter optimization. Our search space consisted of learning rate and batch size. We sampled learning rates from 10<sup>-6</sup> to  10<sup>-4</sup> on log scale and batch sizes were selected from [8, 16, 32]. A total of 50 data points were selected, and for each of them, the model was trained for 5 epochs. 
<center>
<img src="https://portfolio-designs.s3.ap-south-1.amazonaws.com/HPO.png"  height="512" alt="Hyperparameter Optimization Graph">
</center>

**Best Results**
| Learning Rate | Batch Size | Train Accuracy | Validation Accuracy | Train Accuracy | 
| ------ | ------ | ------ | ------ | ------ |
| <center>0.00051868928942</center> | <center>32</center> | <center>71.875</center> | <center>57</center> | <center>60.2</center> |

## Results

#### Food-101

| Model | Learning Rate| Batch Size | Validation acc.(%) | Test acc.(%) |
| ------ | ------ | ------ | ------ | ------ |
| Resnet18 | 0.0001 | 32 | 83.76 | 79.10 | 
| Densenet121 | 0.0005 | 32 | 79.70 | 82.67 |
| MobileNetv2 | 0.00001 | 32 | 94.19 | 96.67 |

<br>
<br>
<center> <b>Accuracy</b> </center>


| ResNet | DenseNet |  MobileNet |
| ------ | ------ | ------ |
|![](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/dense/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/res/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/tf_dt_mobilenet/acc.png) |

<br>
<center> <b>LOSS</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/dense/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/res/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/tf_dt_mobilenet/loss.png) |

<br>
<center> <b>Confusion Matrix</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/dense/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/res/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/tf_dt_mobilenet/conf.png) |




<br>
<center> <b>TSNE</b> </center>


|  | |  |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/dense/tsne.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/res/tsne.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food101/tf_dt_mobilenet/tsne.png) |


#### Food-11k

| Model | Learning Rate| Batch Size  | Validation acc.(%) | Test acc.(%) |
| ------ | ------ | ------ | ------ | ------ |
| Resnet18 | 0.0001 | 32  | 83.76 | 79.10 | 
| Densenet121 | 0.0005 | 32 | 79.70 | 82.67 |
| MobileNetv2 | 0.00001 | 32  | 94.19 | 96.67 |

<br>
<br>
<center> <b>Accuracy</b> </center>


| ResNet | DenseNet |  MobileNet |
| ------ | ------ | ------ |
|![](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/dense/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/res/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/mobile/acc.png) |

<br>
<center> <b>LOSS</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/dense/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/res/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/mobile/loss.png) |

<br>
<center> <b>Confusion Matrix</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/dense/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/res/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/food11k/mobile/conf.png) |


#### World Cuisine

| Model | Learning Rate| Batch Size  | Validation acc.(%) | Test acc.(%) |
| ------ | ------ | ------  | ------ | ------ |
| Resnet18 | 0.0001 | 32 | 54.5 | 53.06 | 
| Densenet121 | 0.0005 | 16 | 60.63 | 59.49 |
| MobileNetv2 | 0.0001 | 32 | 60.13 | 44.46 |

<br>
<br>
<center> <b>Accuracy</b> </center>


| ResNet | DenseNet |  MobileNet |
| ------ | ------ | ------ |
|![](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/dense/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/res/acc.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/mobile/acc.png) |

<br>
<center> <b>LOSS</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/dense/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/res/loss.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/mobile/loss.png) |

<br>
<center> <b>Confusion Matrix</b> </center>


| | | |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/dense/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/res/conf.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/mobile/conf.png) |




<br>
<center> <b>TSNE</b> </center>


|  | |  |
| ------ | ------ | ------ |
|![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/dense/tsne.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/res/tsne.png) |![enter image description here](https://portfolio-designs.s3.ap-south-1.amazonaws.com/results/world/mobile/tsne.png) |




