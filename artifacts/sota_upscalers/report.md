# SOTA Upscalers

*Latex is nice, but i like markdown more ;)*

## Introduction

This is my artifact for the selected SOTA upscalers: DRCT-L, HMANet, & Hi-IR.

This will mainly cover a brief overview of each paper & why it's SOTA (discoveries, impact, etc).

## Background

Most of these papers tackle Simple Image Super-Resolution (SiSR), which mainly involves training a model to upscaling input images, then using it to upscale 'ground-truth' samples during inferencing. Unlike some other vision tasks in machine learning, super resolution is fairly well established, so almost all of these papers use the same datasets for training & inferencing (or at least with significant overlap). 

For the same reason, most papers also use the same two training methods - first they train a 'standard' super solution model (normally with L1Loss), then they fine tune it with a discriminator in a GAN training loop to generate "real" super-resolution images.

## Papers

### DRCT-L

#### Summary

 - DRCT-L is an enhanced version of the Dense-Residual-Connected Transformer, a model built for SISR that was made in the author's previous paper. 
 - The whole point of DRCT-L (and DRCT by extension) is that they try to tackle what they call the 'information bottleneck', where deep networks lose important image details as they process data, especially when using filters in CNN based solutions.
 - To solve this, DRCT-L uses dense connections and Swin Transformer layers to keep these details intact, producing clearer images while (hopefully) using less computing power than other top models.

#### Reasoning

 - The creators of DRCT-L noticed that in many SISR models, the feature maps weaken as the network gets deeper. They argue that this goes beyond just residual connections, and is a fundamental problem of most models because they only see features within filters and that limits the scope of what can be processed.
 - DRCT-L solves this with dense connections, which act like extra pathways to keep information flowing between layers. This is in combination with Swin Transformer layers, which look at both small patches and the entire image to capture details and patterns. 
 - DRCT-L is a larger version of the original DRCT, designed to handle complex images while staying efficient, aiming to beat their main competitor model HAT-L, a bigger version of another advanced model.


#### Findings
 - DRCT-L performs exceptionally well on the standard super-resolution image datasets. 
 - Visually, DRCT-L produces sharper images, like clear building outlines, where other models create blurry results. It maintains this edge even when scaled up, using less memory and computing power. 

### HMANet

#### Summary

 - Their main contribution is a combination of Residual Hybrid Transformer Blocks (RHTB) and Grid Attention Blocks (GAB) to capture both small details and big picture patterns in images.
 - A special pre-training method helps HMANet learn better, making it outperform other top models while staying fairly efficient.

#### Reasoning

 - HMANet uses RHTB to blend local and global information - tries to combine the strengths of CNNs and Transformers.
 - GAB looks at sparse, spread-out image parts to find similarities without needing too much computing.
 - Pre-training on different image scales (like x2, x3, x4) allows the model to gain multiple perspectives on the same image. 

#### Findings
 - Uses more resources (parameters / multiadds) than SwinIR but produces sharper images.

### Hi-IR

#### Summary
 - Hi-IR is a novel image restoration (IR) method designed to recover high-quality images from degradations like noise, blur, or low resolution. 

 - Unlike convolutional neural networks (CNNs) and vision transformers (ViTs), which struggle with efficiency or generalization across tasks, Hi-IR employs a hierarchical information flow mechanism. 

 - It processes images in three stages: analyzing small patches for local details (L1), grouping them into larger patches for broader structures (L2), and integrating global context via efficient convolutions (L3) (balances speed and effectiveness). 

 - To handle larger models, Hi-IR uses training warm-up and lightweight operations, enabling it to scale up without performance loss. 

 - Experiments show it excels in seven IR tasks, including super-resolution and deblurring, while adapting to various degradation types with a single model.


#### Reasoning
 - The reasoning behind Hi-IR addresses key IR challenges. 
 - CNNs are limited by small filters that hinder long-range information sharing, requiring deep, slow networks. 
 - ViTs use global attention but face quadratic complexity, making them computationally expensive for large images. 
 - Window-based methods like SwinIR reduce complexity but struggle with global context. 
 - Hi-IR’s hierarchical flow acts like assembling a puzzle
    1. L1 captures local details
    2. L2 connects medium-sized regions
    3. L3 ensures a global view, avoiding heavy computation. 
 - Scaling issues, where larger IR models often underperform, are mitigated by warming up training for 50,000 iterations and replacing bulky convolutions with lighter alternatives, stabilizing performance.

#### Findings
 - Hi-IR’s findings highlight its superiority. 
 - It outperforms state-of-the-art methods in seven tasks: super-resolution, denoising, JPEG artifact removal, demosaicking, defocus and motion deblurring, and adverse weather IR. 
 - Its hierarchical design achieves global information propagation with lower computational cost than window attention, as shown by its space and time complexity. 
 - Scaling from 15 to 57 million parameters improves PSNR on datasets like Set5, unlike unscaled models that degrade. 
 - A single Hi-IR model handles multiple degradation types and intensities, proving its versatility and generalizability.
