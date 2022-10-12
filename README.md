# DataDriven-Bias-Detection

This directory implements data driven methods for bias classification. It was generated over the duration of the course _Deep Learning_ at ETH Zürich, which was supervised by Prof. Fernando Perez Cruz. The original goal of the project was to implement and test the IFBID architecture for Bias Classification, as proposed in https://arxiv.org/abs/2109.04374.

Colaborators:
- https://github.com/ghjuliasialelli
- https://github.com/LucaSchweri
- https://github.com/schererdavid

For detailed information on the paper, see the submission [paper](https://github.com/travelingtomat0/DataDriven-Bias-Detection/blob/main/Deep_Learning_Report.pdf).

# Usage

To use this directory as a standalone, eg. to reproduce MNIST results or our personal findings, 

## Prerequisites
__First__, the requirements, which need to be installed / upgraded:
- torch
- pytorch-lightning
- sklearn
- tensorflow

## Bias Classifiers: Training

To obtain the bias-classifiers, it is necessary to reproduce (i.e. train the classifiers). To do this, run:
```
python trainer.py --epochs [num_epochs] --stepsize [1 for 100% train data, 10 for 10%] --model_number [number] [path-to-data]
```
Furthermore, it is possible to supply a model number, where:
- 0 corresponds to Dense
- 1 corresponds to Conv
- 2 corresponds to the (adapted) Conv model used for refinement

Further, calling trainer.py has the options:
- Setting the flag **--use_dense** will make the classifier recognise and use the dense layers of the MNIST classifier. **Do not use this flag when reproducing the original IFBID paper!**
- Setting the flag **--reshuffle** will force the reshuffling of the train- and test-dataset. In case different inititalisations have been used (batch-wise) when training the MNIST digit classifiers (for the train and test-dataset), this may improve bias classifier results.

The models will be stored in the directory [path-to-data]/bias_classifiers. An example call would therefore be:
```
python3 trainer.py --model_number 0 --epochs 1 --stepsize 1 --reshuffle --use_dense ./data/author_dataset
```

## Bias Classifiers: Refinement
For **refinement** of the classifiers in the list above, use:
```
python3 refiner.py --epochs [num-refinement-epochs] --model_number [number] [path-to-original-model_weights] [path-to-generalization_dataset] [path-to-bias_classifiers]
```

Further, calling refine.py has the options:
- Setting the flag **--test_on_old** will use the original (authors) test-set for training and refinement.
  - Omitting the flag will refine and test using the generalisation set.
- Setting the flag **--use_dense** will use the classifier that recognises and uses information from the dense layers of the MNIST classifier.
- Model numbers correspond to:
  - 0: Conv Model
  - 1: Dense model

An example call:
```
python3 refiner.py --epochs 1 --model_number 0 --use_dense ./data/author_dataset ./data/generalization_dataset ./data/author_dataset
```
