---
title: CLIP Guided Diffusion
date:   2021-12-18
permalink: /clip-guided-diffusion/
---

## CLIP Guided Diffusion - A Quick Intro

Like many (many!) others, I've been playing around recently with systems that can create 'AI art', mostly with one called "CLIP Guided Diffusion". I didn't come up with this idea or write this code myself; credit for that goes largely to [Katherine Crowson](https://twitter.com/RiversHaveWings) and the Collab notebooks she has been releasing to the world. I'm running code derived from those (but doing so locally).

What is CLIP Guided Diffusion, you ask? In a sentence, it is a system that takes a piece of text and creates images that it thinks are a good representation of that text.

![CLIP Guided Diffusion](/images/clip-guided-diffusion.png)

How does this work? Here's a brief explainer: There are two models at the heart of the system. The first one, CLIP, is [a model](https://github.com/openai/CLIP) released by [OpenAI](https://openai.com/). The special thing about CLIP is that it was trained on a lot of image / caption pairs in such a way that it encodes both images and text into a common vector space, attempting to keep the representations of the pairs close by in that space. So for example if I create embeddings of the words 'dog', 'canine', and a picture of a dog, these will all be fairly close in this vector space, while the text 'house' and a picture of a house would be off in another area of the vector space.

Now if we couple CLIP with a second model that can generate images and that we can backpropagate through, we can give that text to CLIP and it can iteratively 'guide' the generative model towards images that are near the embedded text prompt in our representational space.

For those interested, [LJ Miranda](https://ljvmiranda921.github.io/) has some nice historical notes on the players who created this concept, relevant references, and a more in-depth explanation of how the earlier VQGAN-CLIP code works [in this post](https://ljvmiranda921.github.io/notebook/2021/08/08/clip-vqgan/). (2022-01-03 edit: [This post](https://ml.berkeley.edu/blog/posts/clip-art/), by Charlie Snell, gives a really good historical overview of the various approaches and how they came together in 2021, but it predates the guided diffusion approach.) CLIP Guided Diffusion is conceptually the same as VQGAN-CLIP but uses a different type of model to do the image generation: [Guided Diffusion](https://github.com/openai/guided-diffusion) (also released by OpenAI). From what I've seen, the guided diffusion approach to generating images seems to be more expressive and visually coherent than VQGAN.

The code I've been running lately is based on [this Collab](https://colab.research.google.com/drive/1FuOobQOmDJuG7rGsMWfQa883A9r4HxEO?usp=sharing), which has done a great job speeding up Ms. Crowson's [CLIP Guided Diffusion notebook](https://colab.research.google.com/drive/12a_Wrfi2_gwwAuN3VvMTwVMz9TfqctNj). I generate about one 256x256 image per minute on my middle-of-the-road GTX 1070 GPU (I can't generate 512x512 with my limited GPU memory).

My routine is to get my machine working on maybe 50 or 100 images from one text prompt (overnight or when I'm stepping away for a bit). I then select the ones I like best (which is typically about 5 - 10% of them) and run those through (the very impressive) [Real-ESRGAN super resolution model](https://github.com/xinntao/Real-ESRGAN) to increase the size to 1024x1024.

What follows is a quick tour through some of my favorite images after having played with this for a few weeks. My focus here is on the art created by the AI more so than the prompt engineering that is behind the creations. Rather than identifying the specific prompts used to create each image, I'm using CLIP by itself to do searches through my collection of ~500 favorites. As we go I'll provide a bit of commentary about prompt engineering and the interesting ways in which CLIP sometimes behaves.

## Victorian Era Portrait of a Woman

Let's start with this search: "Victorian Era Portrait of a Woman". So again, I'm asking CLIP to find (in my collection of 500 favorites) the images it thinks most accurately match that phrase.

![Victorian Era Portrait of a Woman](/images/array-victorian.png)

And in this case, the first 5 images CLIP selected were in fact created using that prompt or one very similar (e.g., "Victorian era portrait"). The last image, it turns out, was created with the prompt "Window into a beautiful soul #artstation", but you can see how it's not _too_ bad a match for a Victorian era portrait!

## Beautiful Orchid

Here CLIP is finding the images in my favorites that it thinks most closely match "beautiful orchid".

![Beautiful Orchid](/images/array-beautiful-orchid2.png)

And in fact all of these images were produced with that prompt or a similar one (e.g., "beautiful orchid #artstation" or "watercolor of an orchid").

## Beautiful Colorful Fish

![Beautiful Colorful Fish](/images/array-beautiful-colorful-fish.png)

They are beautiful. And colorful! And all created with the prompt "beautiful colorful fish (trending on artstation)".

## Beautiful Pattern

![Beautiful Pattern](/images/array-beautiful-pattern.png)

## Eye of Sauron

![Eye of Sauron](/images/array-eye-of-sauron.png)

## Child's Drawing

![Child's Drawing](/images/array-childs-drawing.png)

Images 1, 2, 3, and 6 were from the prompt "Mommy and Daddy, drawn by a child". Image 4 was "watercolor painting of an owl". Image 5 was "alien scribblings on a blackboard". But they're all a decent match for the search term "child's drawing".

## Hotel California

![Hotel California](/images/array-hotel-california.png)

Image 5 was from the prompt "a beautiful winter scene in an old town with Christmas lights (acrylic painting)". The rest were all "Hotel California. You can check out any time you'd like, but you can never leave (trending on artstation)".

You've probably noticed that some of the prompts used to create the images contain stylistic elements, like 'trending on artstation' (see [Trending on Artstation](https://www.artstation.com/?sort_by=trending)) or 'watercolor' or 'acrylic painting'. It turns out that CLIP, in the course of its training, saw enough images with captions containing stylistic information that it now has an opinion about what a watercolor painting is, and can steer the generative model in that direction!

## Owl

![Owl](/images/array-owl.png)

Prompts here were all variants on "owl": "an owl made of voxels", "xray owl", or "watercolor painting of an owl". Can you tell which are which?

## Leaves in Fall

![Leaves in Fall](/images/array-leaves-in-fall.png)

## Shenandoah Mountains

![Shenandoah Mountains](/images/array-shenandoah-mountains.png)

The last image here was actually from an "owl"-based prompt, but it's not a bad fit!

## Old Father Time

![Old Father Time](/images/array-old-father-time.png)

It's cool how some of the Old Father Times incorporate the notion of a clock.

## Sand in the Hourglass

![Sand in the Hourglass](/images/array-sand-in-the-hourglass.png)

The first five here were generated with the prompt "sand in the hourglass #artstation"; the last was "leonardo da vinci invention sketch".

## Old European Town at Christmas time (oil on canvas)

![Old European Town at Christmas time (oil on canvas)](/images/array-old-eu-town-at-christmas-oil.png)

## Paradise on Earth

![Paradise on Earth](/images/array-paradise-on-earth.png)

## Martian Sunrise

![Martian Sunrise](/images/array-martian-sunrise.png)

# Now for a detour into some darker places...

In this 'darker' section, the prompts and the search strings tended to be more abstract. As a result, there's a lot more 'crossover' from one prompt to a different search string. And you'll notice that some images show up in more than one search.

## Dark Night of the Soul

![Dark Night of the Soul](/images/array-dark-night-of-the-soul.png)

## Evil Queen

![Evil Queen](/images/array-evil-queen2.png)

## The Grim Reaper

![The Grim Reaper](/images/array-grim-reaper2.png)

## Mysterious Dark Queen of the Afterlife

![Mysterious Dark Queen of the Afterlife](/images/array-mysterious-dark-queen-of-the-afterlife2.png)

## Monster

![Monster](/images/array-monster.png)

## Feeding the Beast

![Feeding the Beast](/images/array-feeding-the-beast.png)

Several of the prompts here included "by Greg Rutkowski". Greg is a prolific artist whose work you can see on Artstation, and he has a very distinct style. Here too, it seems that CLIP has a pretty good understanding of Rutkowski's style.

## Conquering the Fear Within

![Conquering the Fear Within](/images/array-conquering-the-fear-within.png)

Note that we sometimes get attempts at artist signatures on paintings.

## Abomination

![Abomination](/images/array-abomination.png)

## The Gates of Hell

![The Gates of Hell](/images/array-gates-of-hell.png)

## The Hounds of Hell

![The Hounds of Hell](/images/array-hounds-of-hell.png)

# Let's get back to some lighter fare

## Flower in the Shape of a Heart

![Flower in the Shape of a Heart](/images/array-flower-in-the-shape-of-a-heart.png)

## Window into a Beautiful Soul

![Window into a Beautiful Soul](/images/array-window-into-a-beautiful-soul.png)

I like the doggo through the window. Good boy!

Funny here that image 5 is supposed to be an eye of Sauron, and the prompt for image 6 was "conquering the dark fear within #artstation". Beautiful soul indeed.

## Hearts and Flowers

![Hearts and Flowers](/images/array-hearts-and-flowers.png)

## Love and Marriage

![Love and Marriage](/images/array-love-and-marriage.png)

## The Tree of Life

![Tree of Life](/images/array-tree-of-life.png)

# Finally, full size versions of my favorites (along with the approximate prompt used to create it), some of which haven't shown up in the searches above.

## A Beautiful but Haunting Painting

![A Beautiful but Haunting Painting 1](/images/a-beautiful-but-haunting-painting1.png)

&nbsp;

![A Beautiful but Haunting Painting 2](/images/a-beautiful-but-haunting-painting2.png)

&nbsp;

![A Beautiful but Haunting Painting 3](/images/a-beautiful-but-haunting-painting3.png)

## A Beautiful Flower in the Shape of a Heart

![A Beautiful Flower in the Shape of a Heart](/images/a-beautiful-flower-in-the-shape-of-a-heart.png)

## A Beautiful Mind

![A Beautiful Mind](/images/a-beautiful-mind.png)

## A Beautiful Orchid

![A Beautiful Orchid](/images/a-beautiful-orchid.png)

I love how the orchid is incorporated into her hair!

## Alien Among the Stars

![Alien Among the Stars](/images/alien-among-the-stars.png)

## An Alien Among Us

![An Alien Among Us](/images/an-alien-among-us.png)

## Ascending to Heaven

![Ascending to Heaven](/images/ascending-to-heaven.png)

## A Self Portrait of the AI

![A Self Portrait of the AI](/images/a-self-portrait-of-the-AI.png)

She will fit right in!

## A Watercolor Painting of an Owl

![A Watercolor Painting of an Owl 1](/images/a-watercolor-painting-of-an-owl1.png)

&nbsp;

![A Watercolor Painting of an Owl 2](/images/a-watercolor-painting-of-an-owl2.png)

## Conquering the Dark Fear Within

![Conquering the Dark Fear Within](/images/conquering-the-dark-fear-within.png)

## Diamond Dogs by Bowie

![Diamond Dogs by Bowie](/images/diamond-dogs-by-bowie.png)

Diamond Dogs? I wonder what the connection is here...

## Full Moon

![Full Moon 1](/images/full-moon1.png)

&nbsp;

![Full Moon 2](/images/full-moon2.png)

Not sure what to make of this one.

## I Love You - Hearts and Flowers

![I Love You - Hearts and Flowers 1](/images/i-love-you-hearts-and-flowers1.png)

Good dog!!

&nbsp;

![I Love You - Hearts and Flowers 2](/images/i-love-you-hearts-and-flowers2.png)

## I Love You - Here is a Beautiful Flower

![I Love You - Here is a Beautiful Flower 1](/images/i-love-you-here-is-a-beautiful-flower1.png)

&nbsp;

![I Love You - Here is a Beautiful Flower 2](/images/i-love-you-here-is-a-beautiful-flower2.png)

So many good boys. I did notice that CLIP seems to have seen quite a few dog pictures in training. One thing about this method is that you can watch the image evolve from noise to finished product, and many times you can see in early renditions a ghosty-looking version of something, but then CLIP steers the diffusion in another direction. Quite often those early images seem to feature dogs.

## Love, Hearts, Kisses

![Love, Hearts, Kisses](/images/love-hearts-kisses.png)

I really like how the heart is incorporated into her hair.

## Dark Mistress

![Dark Mistress 1](/images/dark-mistress1.png)

&nbsp;

![Dark Mistress 2](/images/dark-mistress2.png)

Cats, on the other hand, CLIP seems to have a different opinion of!

&nbsp;

![Dark Mistress 3](/images/dark-mistress3.png)

## Dark Night of the Soul

![Dark Night of the Soul](/images/dark-night-of-the-soul.png)

## Mysterious Dark Queen of the Afterlife

(I like this prompt...)

![Mysterious Dark Queen of the Afterlife 1](/images/mysterious-dark-queen-of-the-afterlife1.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 2](/images/mysterious-dark-queen-of-the-afterlife2.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 3](/images/mysterious-dark-queen-of-the-afterlife3.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 4](/images/mysterious-dark-queen-of-the-afterlife4.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 5](/images/mysterious-dark-queen-of-the-afterlife5.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 7](/images/mysterious-dark-queen-of-the-afterlife7.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 8](/images/mysterious-dark-queen-of-the-afterlife8.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 9](/images/mysterious-dark-queen-of-the-afterlife9.png)

&nbsp;

![Mysterious Dark Queen of the Afterlife 6](/images/mysterious-dark-queen-of-the-afterlife6.png)

Wow, CLIP has really seen some things...

## The Grim Reaper

![The Grim Reaper 1](/images/the-grim-reaper1.png)

&nbsp;

![The Grim Reaper 2](/images/the-grim-reaper2.png)

## Old Father Time

![Old Father Time](/images/old-father-time.png)

Old Father Time - as an owl.

## The Planet Saturn

![The Planet Saturn](/images/the-planet-saturn.png)

Not sure why it thinks this is Saturn-like, but I do find it visually pleasing.

## The Tree of Life

![The Tree of Life 1](/images/the-tree-of-life1.png)

&nbsp;

![The Tree of Life 2](/images/the-tree-of-life2.png)

&nbsp;

![The Tree of Life 3](/images/the-tree-of-life3.png)

&nbsp;

![The Tree of Life 4](/images/the-tree-of-life4.png)

## Very Confused Look

![Very Confused Look 1](/images/very-confused-look1.png)

&nbsp;

![Very Confused Look 2](/images/very-confused-look2.png)

This prompt, "very confused look", cracked me up when I first ran it. Half of the images ended up being dogs. Even when the prompt is "Person with a very confused look" you occasionally get a dog thrown in.

[Here is an album](https://photos.app.goo.gl/Xv7FgAAMTEUrUUZe8) with these and more of my favorites.

That's all for now. Thanks for visiting!