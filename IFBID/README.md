
# IFBID Model

The Paper **"IFBiD: Inference-Free Bias Detection"** submitted at the AAAI Workshop on Artificial Intelligence Safety (SafeAI 2022) presents a deep learning architecture for the detection of bias in classifier networks.

The proposed architecture is a convolutional neural network that uses layer weights (not layer biases) to calculate the bias of a classifier on a range 

_[1: very low bias, ..., 4: very high bias]_.

Inputs to the classifier are MNIST digit classifiers which have been trained on the colored MNIST dataset as proposed in **Learning Not to Learn: Training Deep Neural Networks with Biased Data** (https://arxiv.org/abs/1812.10352).

# This Directory

In this directory we implement the IFBID architecture with help of the libraries Pytorch and Pytorch-Lightning. Importantly, **as of now we have only implemented the IFBID architecture for the DigitWB** database. Keep in mind that the MNIST classifiers that are input to the IFBID model have the shape depicted below:

![Required MNIST Classifier Architecture](https://github.com/travelingtomat0/DataDriven-Bias-Detection/blob/main/figs/other_architecture.jpeg?raw=true)

# Usage

