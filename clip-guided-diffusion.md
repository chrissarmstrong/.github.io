---
layout: page
title: Clip Guided Diffusion
permalink: /clip-guided-diffusion/
---

Like many others, I've been playing around creating 'AI art' with CLIP Guided Diffusion. I didn't write this code myself, just running code from one of the many Collab notebooks but doing so locally.

What is CLIP Guided Diffusion, you ask? Very briefly, it is a system that takes a piece of text and uses that to create images that it thinks are a good representation of that text.

How does this work? Here's a brief explainer: CLIP is a model released by OpenAI. The special thing about CLIP is that it was trained on a lot of image / caption pairs in such a way that it encodes both images and text into a vector space, attempting to keep the representations of the pairs close by in that space. So for example if I create embeddings of the words 'dog', 'canine', and a picture of a dog, these will all be fairly close in this vector space.

Now if we couple CLIP with a model that can generate images and that we can backprop through, we can give that text to CLIP and it can iteratively 'guide' the generative model towards images that are near the embedded text in our representational space.

From what I can tell, [Katherine Crowson|https://twitter.com/RiversHaveWings] first wired this up, but originally using a different generative model called VQ-GAN.[^1] She later moved over to the (arguably more expressive and coherent) Guided Diffusion[^2] model.

(I'm running code based on [this Collab|https://colab.research.google.com/drive/1FuOobQOmDJuG7rGsMWfQa883A9r4HxEO?usp=sharing#scrollTo=h4MHBPT1nirT], which has done a great job really speeding things up. I generate about an image per minute on my middle-of-the-road 1070 GPU.)





References:
[^1]: 

[^2]: 
