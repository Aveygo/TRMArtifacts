# Diffusion Models Course Notes

## Unit 1: Intro to Diffusion Models

### Website Notes
- Diffusion models can generative images, audio, etc.
- Works by starting with random noise and refining it iteratively into a final output.
- Process: Add noise to training images in varying amounts, then train the model to denoise them. Model eventually learns to generate data from pure noise.
- To generate new data, start with noise and repeatedly denoise using the trained model.
- Course really likes shilling diffusers library to build and train these models.

### Notebook Notes
 - StableDiffusionPipeline for really fast setup
 - DDPMScheduler (non-linear?)
 - Contains simple training loop, still using diffusers
 - Second notebook is pretty similar but from 'scratch' (still uses diffusers lol)

## Unit 2: Fine-Tuning, Guidance, and Conditioning

### Website Notes
- **Fine-Tuning**: Start with a pre-trained model and tweak it on new data.
- **Guidance**: Modify an unconditional model’s output during generation by using a guidance function (eg, CLIP embeddings).
- **Conditioning**: Feed extra info (like class labels or text) into the model during training to control generation. Includes:
  - Adding info as extra input channels to the UNet.
  - Using embeddings to influence internal UNet layers.
  - Cross-attention for text-based conditioning (used in Stable Diffusion).

### Notebook Notes
 - Nothing too different from Unit 1, just more shilling.
 - wandb looks good for viewing training logs (like tensorboard) but needs an account (!!!) 

## Unit 3: Stable Diffusion (SD)

### Website Notes
 - **SD** is a text-conditioned latent diffusion model that generates images from text prompts.
 - **Latent Diffusion**: Uses a Variational Auto-Encoder (VAE) to compress images into a smaller latent space (e.g., 512px image to 64px latent), reducing computational cost (channel width also increases? Not sure to what. TODO)
 - **Text Conditioning**: Uses CLIP to turn text prompts into embeddings (77 tokens, 1024 dimensions each). Cross-attention layers in the UNet use these to guide denoising.
 - **Classifier-Free Guidance (CFG)**: During training, sometimes skip text conditioning to teach unconditional generation. At inference, combine conditioned and unconditioned predictions to better match the prompt.
 - **SD** can be used for super-resolution, inpainting, and depth-to-image generation by using different types of conditioning.
- **DreamBooth**: Fine-tune SD to learn new concepts using a few images -> isnt this just textual Inversion??? Dreambooth costs money!

## Unit 4: Advanced Topics
- **Faster Sampling**: Progressive distillation trains a "student" model to match a "teacher" model’s output in fewer steps.
- **Training Improvements**:
  - Tune noise schedules and loss weighting for efficiency.
  - Train on diverse aspect ratios or use cascaded models (low-res model + super-res model).
  - Better conditioning with rich text embeddings or multiple inputs.
- **Editing and Control**: Techniques like img2img (add noise, denoise with a new prompt), inpainting (edit specific regions), and cross-attention control for precise edits.
- **Video and Audio**:
  - Video: Treat as image sequences, use 3D UNets, and apply super-resolution for quality.
  - Audio: Convert audio to spectrograms (2D "images"), use diffusion models to generate, then convert back to audio (e.g., Riffusion).
- **New Approaches**: Moving toward "iterative refinement" models (beyond just noise-based diffusion) and using transformers instead of UNets for better performance.

# Summary

This course is so obviously just trying to hook new users into diffusers. Would not recommend. At least they tried with the yt videos and notebooks.

This is very off script but if you're here then you might be interested - I actually used diffusers like 3 years ago before it was cool. I have a niece-in-law who still runs a business selling artworks, and it inspired my sisters into a whole 'artistic-phase', but they were not as good to say the least. I was able to scrape some of her artworks from her site and used textual inversion to 'train' on her images. From there I used the image-to-image feature in Automatic1111 to convert family photos into her style, from which my sisters could copy and learn from. Nowadays it's just done in ChatGPT, but *back-in-ye-old-days* it was a royal pain in the butt - all before vibe coding of course. 