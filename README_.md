# Learning Probability Density Function using GAN

## Student Details

Name: Raunaq Mittal\
Roll Number: 102303752\
Assignment: Learning Probability Density Functions using Data Only

------------------------------------------------------------------------

## Objective

The objective of this assignment is to learn the unknown probability
density function (PDF) of a transformed random variable using a
Generative Adversarial Network (GAN), without assuming any parametric
distribution.

The GAN learns the distribution only from samples of the transformed
variable.

------------------------------------------------------------------------

## Dataset Used

Feature: NO₂ concentration (NO2 column)\
Source: India Air Quality Dataset

Only the NO₂ column was used for this assignment.

------------------------------------------------------------------------

## Step 1: Transformation of Data

The transformation used is:

z = x + a_r sin(b_r x)

Where:

a_r = 0.5 (r mod 7)\
b_r = 0.3 (r mod 5 + 1)

For roll number 102303752:

r mod 7 = 5\
r mod 5 = 2

Therefore:

a_r = 2.5\
b_r = 0.8999

Final transformation:

z = x + sin(0.6x)

The transformed data was normalized before training to improve GAN
stability.

------------------------------------------------------------------------

## Step 2: GAN Architecture

The GAN consists of two neural networks:

### Generator

-   Input: 1D Gaussian noise sampled from N(0,1)
-   Architecture:
    -   Linear(1 → 64)
    -   ReLU
    -   Linear(64 → 64)
    -   ReLU
    -   Linear(64 → 1)
-   Output: Generated sample of z

### Discriminator

-   Input: Scalar value of z
-   Architecture:
    -   Linear(1 → 64)
    -   LeakyReLU
    -   Linear(64 → 64)
    -   LeakyReLU
    -   Linear(64 → 1)
    -   Sigmoid
-   Output: Probability of sample being real

Loss Function: Binary Cross Entropy\
Optimizer: Adam (learning rate = 0.0002)\
Training Epochs: 3000\
Batch Size: 64

The generator attempts to fool the discriminator, while the
discriminator learns to distinguish real and generated samples.

------------------------------------------------------------------------

## Step 3: PDF Estimation

After training:

-   10,000 samples were generated from the trained generator.
-   Histogram density estimation was performed.
-   Kernel Density Estimation (KDE) was applied for smoother PDF
    visualization.
-   The real and generated distributions were compared visually.

No analytical distribution (Gaussian, exponential, etc.) was assumed at
any stage.

------------------------------------------------------------------------

## Observations

### Mode Coverage

The generator captures the main density regions of the transformed data.
The major modes are reflected in the generated samples, indicating
reasonable coverage of the distribution.

### Training Stability

The generator and discriminator losses oscillate during training, which
is expected in GAN training. No severe instability or complete mode
collapse was observed.

### Quality of Generated Distribution

The histogram and KDE plots show significant overlap between real and
generated samples. Minor deviations are visible at extreme tails, but
overall the GAN successfully approximates the unknown distribution.

------------------------------------------------------------------------

## Conclusion

The Generative Adversarial Network successfully learned the probability
density function of the transformed variable using only sample data. The
model was able to approximate the unknown distribution without assuming
any parametric form.

This demonstrates the capability of GANs in implicit density modeling
from data alone.
