# GAN-Based Lyrics Generation with Melody Conditioning and LSTM architecture.

![image](https://github.com/user-attachments/assets/03074cde-cd56-421b-a2a0-fe44d22a52b1)


This project involves the development of a Generative Adversarial Network (GAN) architecture designed to generate song lyrics based on a given melody. The GAN framework integrates a generator, a discriminator, and an LSTM-based recurrent neural network (RNN) to create and evaluate lyrics that align with musical melodies.

## Table of Contents

1. [Introduction](#introduction)
2. [Architecture Overview](#architecture-overview)
3. [Training Procedure](#training-procedure)
4. [Experiments and Results](#experiments-and-results)
5. [Prediction Examples](#prediction-examples)
6. [Summary](#summary)

## Introduction

This project explores the use of GANs in generating song lyrics conditioned on melody information. The architecture combines a generator that creates lyrical content, an RNN (based on a previous implementation) that processes this content, and a discriminator that evaluates the authenticity of the generated lyrics by comparing them to real lyrics associated with the same melody. The project also involves experimenting with different setups where the LSTM's weights are either frozen or fine-tuned during training.

## Architecture Overview

The GAN architecture is composed of three main components:

![image](https://github.com/user-attachments/assets/7d588f31-de45-41b9-881f-f5bc0fc8f40e)


### Generator
The generator receives two inputs: random noise sampled from a Gaussian distribution and melody information extracted from MIDI files. The inputs are concatenated and passed through several dense layers to produce an output vector that represents the generated word embedding, which is then fed into an LSTM to generate the lyrics.
![image](https://github.com/user-attachments/assets/b49fcbe9-ddc0-4aea-9136-5f16460e3ff0)



### LSTM
The LSTM processes the word embeddings generated by the GAN, capturing temporal dependencies and generating the final lyrics. The LSTM architecture consists of multiple layers, including dense layers for higher-level feature extraction and a softmax layer for predicting the next word in the sequence.
![image](https://github.com/user-attachments/assets/6bae2527-2d8c-42d6-aed4-b03e8d63b091)



### Discriminator
The discriminator, an RNN, takes three inputs: the melody information, the real lyrics, and the generated lyrics. These inputs are concatenated and processed through LSTM layers followed by dense layers, ultimately producing a binary classification output that indicates whether the input lyrics are real or generated.
![image](https://github.com/user-attachments/assets/27dc6fd4-cfdd-434d-beb0-6bc4f561d698)



## Training Procedure

The GAN is trained using a combination of the generator, LSTM, and discriminator components. During training, the generator creates lyrics based on random noise and melody input, which are then evaluated by the LSTM and discriminator. The discriminator's feedback is used to update the generator, enabling it to produce more realistic lyrics over time.

Two setups are explored:

- **Setup 1**: The LSTM weights are frozen (non-trainable), retaining the weights from a previous task.
  The GAN hyperparameters:
  - LSTM model's weights = FROZEN
  - Number of Epoch = 100
  - Batch Size = 16
  - Optimizer for generator = Adam
  - Optimizer for discriminator = Adam
  - Learning rate = 0.001
  - Loss = Categorical binary entropy

  ![image](https://github.com/user-attachments/assets/c0377293-9c78-4e3a-9a2d-14f4ebaa45b9)
  ![image](https://github.com/user-attachments/assets/60c6fed8-6efd-4067-a793-1a51861d7e91)


- **Setup 2**: The LSTM weights are trainable, allowing for fine-tuning during training.
  The GAN hyperparameters:
  - LSTM model's weights = TRAINABLE
  - Number of Epoch = 100
  - Batch Size = 32
  - Optimizer for generator = Adam
  - Optimizer for discriminator = Adam
  - Learning rate = 0.001
  - Loss = Categorical binary entropy

  ![image](https://github.com/user-attachments/assets/346d69ed-5f9d-4d04-a9c7-a30c6b1b31ba)
  ![image](https://github.com/user-attachments/assets/20eacd76-fdaf-4884-baa9-1d48dfb24cda)



## Experiments and Results

The experiments involved training the GAN in both setups with different hyperparameters, such as learning rates, batch sizes, and optimizer configurations. The performance of the GAN was evaluated based on the ability of the generated lyrics to mimic real lyrics, as determined by the discriminator's accuracy.

- **Setup 1**: The GAN with frozen LSTM weights showed smoother training loss curves, but limited learning capacity due to the fixed nature of the LSTM.
- **Setup 2**: The GAN with trainable LSTM weights exhibited more volatile training behavior, with mixed results in generating realistic lyrics.

## Prediction Examples

The models were tested on a set of songs, generating lyrics based on the melody. The quality of the generated lyrics was evaluated using n-gram accuracy, comparing the generated lyrics to the real lyrics from the test set. The results varied, with some generated lyrics showing close alignment with the real lyrics, while others diverged significantly.

## Summary

This project demonstrated the challenges and potential of using GANs for lyrics generation conditioned on melody. While the generated lyrics did not consistently match the quality of real lyrics, the project provided valuable insights into the complexities of integrating GANs with RNNs in a musical context. The experience gained from this project lays the foundation for further exploration of generative models in creative applications.

