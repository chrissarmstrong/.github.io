---
layout: page
title: Clip Guided Diffusion
permalink: /clip-guided-diffusion/
---

Like many (many!) others, I've been playing around recently with systems that can create 'AI art', mostly with one called "CLIP Guided Diffusion". I didn't write this code myself, I'm just running code from [Katherine Crowson's|https://twitter.com/RiversHaveWings] Collab notebook but doing so locally.

What is CLIP Guided Diffusion, you ask? Very briefly, it is a system that takes a piece of text and create images that it thinks are a good representation of that text.

How does this work? Here's a brief explainer: There are two models at the heart of the system. CLIP is a model released by OpenAI. The special thing about CLIP is that it was trained on a lot of image / caption pairs in such a way that it encodes both images and text into a common vector space, attempting to keep the representations of the pairs close by in that space. So for example if I create embeddings of the words 'dog', 'canine', and a picture of a dog, these will all be fairly close in this vector space, while the text 'house' and a picture of a house would be off in another area of the vector space.

Now if we couple CLIP with a model that can generate images and that we can backpropagate through, we can give that text to CLIP and it can iteratively 'guide' the generative model towards images that are near the embedded text in our representational space.

LJ Miranda has some nice historical notes on the players who created this concept, relevant references, and a more in-depth explanation of how the earlier VQGAN-CLIP code works [in this post|https://ljvmiranda921.github.io/notebook/2021/08/08/clip-vqgan/]. Clip Guided Diffusion is conceptually the same but uses a different type of model to do the image generation.

I'm running code based on [this Collab|https://colab.research.google.com/drive/1FuOobQOmDJuG7rGsMWfQa883A9r4HxEO?usp=sharing#scrollTo=h4MHBPT1nirT], which has done a great job really speeding up Katherine's [CLIP Guided Diffusion notebook|https://colab.research.google.com/drive/12a_Wrfi2_gwwAuN3VvMTwVMz9TfqctNj#scrollTo=X5gODNAMEUCR]. I generate about one 256x256 image per minute on my middle-of-the-road GTX 1070 GPU (I can't generate 512x512 with my limited GPU memory). The guided diffusion approach to generating images seems to be more expressive and visually coherent than VQGAN.

My routine is to get my machine working on maybe 50 or 100 images from one text prompt (overnight or when I'm stepping away for a bit). I then select the ones I like best (which is typically about 5% of them) and run those through (the very impressive) [Real-ESRGAN super resolution model|https://github.com/xinntao/Real-ESRGAN] to increase the size to 1024x1024.

What follows is a quick tour through some of my favorite images, followed by a demonstration of image search also powered by CLIP.

| 'images/prompt--a view of the shenandoah mountain range in fall with the leaves turning pretty colors_iteration--00039_seed--1466498239_out.png' |   |   |
|--------------------------------------------------------------------------------------------------------------------------------------------------|---|---|
| ![Shenandoah Mountains]('images/prompt--a view of the shenandoah mountain range in fall with the leaves turning pretty colors_iteration--00039_seed--1466498239_out.png' "Shenandoah Mountains")                                                                                                                                                 |   |   |
|                                                                                                                                                  |   |   |
|                                                                                                                                                  |   |   |

![Shenandoah Mountains]('images/prompt--a view of the shenandoah mountain range in fall with the leaves turning pretty colors_iteration--00039_seed--1466498239_out.png' "Shenandoah Mountains")
