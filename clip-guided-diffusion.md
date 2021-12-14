---
layout: page
title: Clip Guided Diffusion
permalink: /clip-guided-diffusion/
---

Like many others, I've been playing around creating 'AI art' with CLIP Guided Diffusion. I'm not doing anything special here, just running code from one of the many Collab notebooks but doing so locally.

What is CLIP Guided Diffusion? In a sentence, it is a system that takes a piece of text and uses that to create images that it thinks are a good representation of that text.

How does this work? There are some good explanations around, but I'll give a brief explainer: CLIP is a model released by OpenAI. The special thing about CLIP is that it was trained on a lot of image / caption pairs in such a way that it encodes both images and text into a vector space, attempting to keep the representations of the pairs close by in that space.

So for example if I create embeddings of the words 'dog', 'canine', and a picture of a dog, these will all be fairly close in this vector space.

Now if we couple CLIP with a model that can generate images and we can backprop through, we can give that text to CLIP and it can iteratively 'guide' the generative model towards images that are near the embedded text in our representational space.

References:
