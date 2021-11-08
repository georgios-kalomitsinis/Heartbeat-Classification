# Heartbeat-Classification

The present work aims to classify heartbeats as accurately as possible into four types using neural networks. The dataset used for both the training and the evaluation of the developed model comes from the [Physionet competition](https://physionet.org/content/challenge-2017/1.0.0/) held in 2017. In specific, we explore deep learning architectures that aim to identify electrocardiograms (ECGs) into 4 different categories: 

1) N : Normal Rhythm
2) A : Atrial Fibrillation Rhythm
3) O : Other Rhythm 
4) ~ : Noisy Recording 

<p align="center">
<img src="https://user-images.githubusercontent.com/80779522/140652032-7328cc32-3e48-4567-818f-f863c0d99d0b.png" />
<figcaption align = "center"><p align="center">
  Figure 1. Data profile for the training set. </figcaption>
</figure>

<p align="center">
<img src="https://user-images.githubusercontent.com/80779522/140652031-3cb21760-b83e-4158-bb52-b43ff4dccbce.png"  />
<figcaption align = "center"><p align="center">
  Figure 2. Examples of the ECG waveforms.</figcaption>
</figure>

The training of the Convolutional Neural Networks (CNNs) took place in 6048 time series, while the validation in 1513 (ie 20% of the original dataset). For the evaluation (testing) of the CNNs, the validation set of the competition was used that consists of 260 heart rate signals. 

## Preprocessing

The length of the signals varies from 2700 to 18300 points. Based on this and to reduce the class imbalance it is chosen to sample the data based the average length (9000). The data is fed to the model in sections of 20 channels with 450 points each. Afterwards, the method ```LabelEncoding``` was used in order to convert each value in a column to a number. 

<div align="center">
  
| N | A | O | ~ |
| :---: | :---: | :---: | :---: | 
| 0 | 1 | 2 | 3 |
  
</div>
<figcaption align = "center"><p align="center">Table 2. The labels for each class.</figcaption>
</figure>

## Methodology

The aim of this work is the design of a neural network and the selection of that architecture as well as its parameters that will be the most accurate, after a series of experiments. There are many possible combinations that can occur. For this reason, the ultimate goal was to develop the least possible degree of architectural complexity with the greatest accuracy. Accuracy is defined as:

<div align="center">
  
![equation](https://latex.codecogs.com/gif.latex?%5Cbg_white%20Accuracy%20%3D%20%5Cfrac%7BTP&plus;TN%7D%7BTP&plus;TN&plus;FP&plus;FN%7D)
</div>
where TP, TN, FP, FN corresponds to True Positives, True Negatives, False Negatives and False Positives, respectively. The examined parameters are:

* the convolutional layers
* the pooling layers
* the number of the connected layers
* activation functions
* batch size
* learning rate
* dropout

## Results

The search for the appropriate hyperparameters leads us to choose the following arcitecture with:
* convolutional layer (*filters=8*)
* maxPooling layer (*pool_size=(3,1)*)
* convolutional layer (*filters=16*)
* maxPooling layer (*pool_size=(4,1)*)
* convolutional layer (*filters=8*)
* maxPooling layer (*pool_size=(2,1)*)
* dense layer (*filters=128, dropout=0.1*)
* dense layer (*filters=64, full-connected*)
* batch_size=16
* learning_rate=0.0001
* and Rectified Linear Unit (ReLu) as activation functions


<p align="center">
<img src="https://user-images.githubusercontent.com/80779522/140654522-5f6f0e5f-41ae-4061-8ba4-dbc3139d5364.png"  />
<figcaption align = "center"><p align="center">
  Figure 3. Suggested architecture.</figcaption>
</figure>


<p align="center">
<img src="https://user-images.githubusercontent.com/80779522/140707773-18b4ed4c-84d8-4192-bbc1-f9d6ea71c066.png"  />
<figcaption align = "center"><p align="center">
  Figure 4. ROC curves.</figcaption>
</figure>

