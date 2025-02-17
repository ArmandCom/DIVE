# Disentangled Imputed Video autoEncoder (DIVE)

The following code is an implementation for Scenario 3 in the experiments of the paper:
"Learning Disentangled Representations of Video with Missing Data"


Missing data poses significant challenges while learning representations of video sequences.
We present DIVE, a deep generative model that imputes and predicts future video frames in the presence of missing data.
Specifically, DIVE contributes by:
- Introducing a missingness latent variable,
- Disentangles the hidden video representations into static and dynamic appearance, pose, and missingness factors for each object and
- Imputing each object trajectory where data is missing.
This is done in an end-to-end training fashion and with using only self-supervision, by leveraging a VAE framework.

## Demo

### Deformed and Missing-Data Moving MNIST

We prepare the code to be trained and tested for scenario 3 of the experiments for Moving MNIST which includes:
- Out-of-scene (fully occluded) digits for 1 time-step
- Varying appearance following an elastic transformation, which is reduced linearly in time from very severe (alpha = 100) to inexistent.
All arguments are set by default for this scenario, but they can be changed at the users convenience. To better understand them, use the help command "-h" or refer to the "config.py" file.
For this experiment, missing labels are set to be soft.

A qualitative example of the expected results after 600 epochs (about 100k iterations) is:
<img src="example_image_varying_MNIST.png" width="800px"/>

After setting up the environment, we can train and test the code with:
```
cd DIVE/
python3 train.py
```
and
```
python3 eval.py
```
To view the results (while training in this case), execute the following commands:
```
cd tensorboard/ckpt/moving_mnist/dive/
tensorboard --logdir train_log --port 6006
```

## Installation
This codebase is trained and tested with Python 3.6+, Pytorch 1.2.0+ and Cuda 10.0+. We use tensorboardX 2.0. for visualization purposes.
We make use of [Pyro](http://pyro.ai/) 0.2 as our framework for probabilitstic programming. To better understand our model, we encourage the reader to browse their [Examples and Tutorials](https://pyro.ai/examples/).

### Moving MNIST
Download MNIST dataset from by running:
```
cd DIVE
mkdir moving_mnist
cd moving_mnist
wget http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
```
For this demo we can't provide our fixed test set. Instead we use an on-the-fly generated set for testing.

## Citations
This code uses as its skeleton the available implementation for Decompositional Disentangled Predictive Auto-Encoder ([DDPAE](https://github.com/jthsieh/DDPAE-video-prediction)), as well as many of its functions, while it is built on Pyro.
