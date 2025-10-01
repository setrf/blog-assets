---
title: On bananas and tourists from the matrix
author: Mert Gulsun
date: 2025-08-31T04:36:00.000Z
slug: on-bananas-and-tourists-from-the-matrix
---

Last weekend my dear friend Barış and I went down to Santa Cruz. I am slowly uncovering that Bay Area has an interesting geography, so an hour in the car is often all it takes to go from snow-bright ridgelines to a beach with glitter on the water. 

We found a great coffee spot, and let the ocean do that reset thing it does.

![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-bananas-and-tourists-from-the-matrix/images/img-9484-jpeg-2608d6e5.jpeg)![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-bananas-and-tourists-from-the-matrix/images/img-9500-medium-jpeg-2608d6e5.jpeg)

Back home that night I scrolled through our shots while my tech-infested timeline kept feeding me demos and papers. That is when the thought landed. We had driven an hour to change the backdrop. With the newest tools popping out I could be even faster.

I had been playing with Nano Banana (a compact image model that shocked the community, later revealed to be [Gemini 2.5 Flash Image](https://developers.googleblog.com/en/introducing-gemini-2-5-flash-image/)). Same hair and earrings, same jacket and little quirks, carried from one scene to the next. It felt like moving a paper cutout version of a person across a stack of postcards.

That tugged a thread back to the StyleGAN era. StyleGAN introduced a style-based generator that separates high-level attributes like identity and pose from finer stochastic detail, which is why you can tweak one without wrecking the other. [The original paper ](https://arxiv.org/abs/1812.04948)spells this out and shows how the architecture improves interpolation and disentanglement across scales.

Around the same time, thispersondoesnotexist turned that research into a cultural moment. [Tom Roelandts has a clear explainer](https://tomroelandts.com/articles/this-person-does-not-exist) of how GANs pit a generator against a discriminator and why that feedback loop can produce such convincing faces, while also noting the little quirks you sometimes spot on a hard refresh.

There is a serious footnote too. Research has shown that identity information can leak from training data into synthetic faces, even without malicious intent. [The WACV 2021 paper “This Face Does Not Exist … But It Might Be Yours!” ](https://arxiv.org/abs/2101.05084)evaluated StyleGAN2 generations with several matchers and found evidence of identity leakage. That reminder sits in the back of my head whenever I tinker. 

So I gave myself a small quest. By the powers granted to me by the long-weekend, a generous API access from Google, and Github Student Pack’s DigitalOcean credits loaded on to a 5 USD VPS (and Codex CLI loaded on to it), I rolled up my sleeves.

I spun up the tiny DigitalOcean VPS droplet, pointed a simple pipeline at a batch of synthetic faces, curated a list of famous landmarks, and asked Nano Banana to place a consistent character into each scene. Keep it lightweight. Keep it playful. Avoid repeating the same face with the same place so the tour feels fresh.

With a little bit of back-and-forth, [**thistouristdoesnotexist**](https://thistouristdoesnotexist.com/) was live. 

Refresh, and a synthetic traveler appears at a landmark. Refresh again, and another character shows up somewhere new. It feels like a scrapbook from a parallel trip never taken.

![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-bananas-and-tourists-from-the-matrix/images/image-png-2608d6e5.png)![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-bananas-and-tourists-from-the-matrix/images/image-png-2608d6e5.png)

A few things stood out while I was play-testing:

- Character identity holds steady from scene to scene. Hair, accessories, and proportions carry over.- Architecture survives with more fidelity than I expected. Domes, arches, filigree, and skyline edges read as the real location rather than a generic backdrop.- Poses and light usually make sense. The stance looks like a tourist pose, shadows fall in the right direction, and reflections often line up with the environment.
There are wobbles. A stray hand blends into a railing. A face drifts slightly. I smile when that happens, because it reminds me that these tourists are stitched from matrix multiplications on a TPU, not post-cards from a friend.

The Bay Area makes quick physical travel feel normal. Tools like this make quick imaginary travel feel normal too. I am not trying to replace the feeling of wind on the pier in Santa Cruz. I am sketching with photons and letting a virtual traveler hop from the Hagia Sophia to Chichén Itzá in seconds.

Have fun sending these virtual people on a joyride around the world. If you find a favorite, I would love to see it!