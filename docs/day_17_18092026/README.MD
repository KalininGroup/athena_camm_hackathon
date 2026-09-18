# Hackathon: Structure → Property Challenge

## What is the data?

In this challenge, we have **two types of information measured at the same locations on a sample**:

* A **structural image** — showing what the material looks like locally.
* An **EELS spectrum** — showing the measured spectral response of the material at each location.

Think of the dataset as a map. For every position \((x,y)\), we have both:

**Local Structure → EELS Response**

The main question of the hackathon is:

> **Can we use what the material looks like locally to predict its EELS response?**

---

## Making the problem simpler

An EELS spectrum contains many values, which can make prediction complicated.

Instead, we can summarize part of the spectrum using **one number**, called a **scalarizer**.

For example, we can select an energy range of interest and calculate the total EELS intensity inside that region.

So now, at every position, we have:

**Image Patch → Scalarizer**

The scalarizer calculated directly from the measured EELS data is our **ground truth** — the value we want our model to predict.

---

## What will we do?

Instead of giving the model only one image pixel, we take a small **image patch** around each location. In the starting example, this is a **5 × 5 pixel patch**.

Our prediction pipeline is:

**Image Patch → Descriptor → Regressor → Predicted EELS Scalarizer**

### 1. Build a descriptor

A **descriptor** converts the image patch into a few meaningful numbers.

For example, the starter descriptor measures:

* average intensity
* intensity variation
* intensity range

The main challenge is to think of **better ways to describe the local structure**.

### 2. Train a regressor

The **regressor** learns the relationship between those structural descriptors and the measured EELS scalarizer.

We train the model using part of the data and test it on data it has not seen before.

---

## How will we compare solutions?

We are not simply looking for the most complicated model.

We want a solution with a good balance of:

**Predictive Power** — Does it accurately predict the measured EELS response?

**Simplicity** — Can we make the prediction using only a small number of features?

**Explainability** — Can we understand what the descriptor measures and why it may be related to the EELS response?

Prediction quality will be measured using **R²**, where a higher value means better agreement between the prediction and the measured data.

We will test different **descriptor + regressor combinations**, compare their R² values, and identify the most useful combinations.

## Final Goal

> **Find the simplest, most explainable description of the local image structure that can still predict the EELS response well.**

The important question is not only **“Can we predict it?”**, but also:

> **“What structural information in the image is actually connected to the measured material response?”**
