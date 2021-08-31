# Roof Detection on Satellite Images

## Problem
* Field: Computer Vision
* Task: Semantic Segmentation Problem (binary): 
  * Input: Satellite Photo, (256,256,3) 
  * Output: 2D B/W grid, (256,256,1) 

## Image processing
* X: Sharpening (Kernel Convolution) and Normalization
* Y: Normalization

## Data Augmentation

* keras.preprocessing.image.ImageDataGenerator:
  * Rotation range = **45°**
  * Width shift range = **0.1**
  * Height shift range = **0.1**
  * Zoom range = **0.2**
  * Horizontal flip = **True**
  * Vertical flip = **True**
* Provide the same random seed and keyword arguments to the fit and flow methods

## Network Architecture


#### Fully Convolutional Networks (e.g. U-Net)
1. Networks without any dense layers and only convolution and pooling layers
2. Takes an input image and outputs a segmentation map of same size
3. Computationally expensive because of the number of FLOPs required to process an image => an encoder architecture

#### Architecture
- Model: **U-Net**  ([source](github.com/SaveraLLC/Indian-rooftops-detection))
- Optimizer: **Adam**
- Loss function: **Binary Cross-Entropy and Dice Loss** or **F1-loss (F1-score)**
- Metric: **Dice Loss** or **F1-score**

#### Hyperparameters
- Batch Size: **16**
- Steps per training epoch: **20** (size of training dataset)
- Validation steps: **4** (size of validation dataset)
- Epochs: about **50**

#### Callbacks
* **Checkpoints**
  * Saves the model weights, epoch with lowest validation loss
* **Reduce Learning Rate**
  * Reduce learning rate if validation loss does not decrease for 1 epoch
* **Early Stopping**
  * Training stops if validation loss does not change for 20 epochs


