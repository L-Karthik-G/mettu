---
title: "Deep Filtering: Listening to the Universe with AI"
date: "2026-02-12"
layout: "post"
tags:
    - "Science"
---

My interest in science and astrophysics, combined with a growing fascination for machine learning, led me to explore a model that brings the best of both worlds together. In this blog, I’ll share what I’ve learned and walk you through how machine learning is now being used to make scientific tasks faster, smarter, and more efficient.

---

# LIGO

LIGO is the Laser Interferometer Gravitational-Wave Observatory. It’s an observatory that doesn’t look at light, stars, or planets the way a normal telescope does. Instead, it listens to the universe.

Have you ever read an article about a newly discovered black hole where scientists somehow know how massive it is or how big it might be? It almost feels like guesswork, right? But it isn’t.

What LIGO detects are gravitational waves, tiny ripples in spacetime caused by massive events like black holes colliding. When two huge objects interact, they disturb spacetime itself, and that disturbance travels all the way to Earth.

Think of it like this: if you drop a rock into still water, waves spread out from the point of impact. Now imagine spacetime behaving like that water. Those ripples are what LIGO is designed to detect.

---

### So how does LIGO actually measure and store this data?

At its core, LIGO uses lasers. It has two long arms placed perpendicular to each other. A laser beam is split into two, sent down both arms, reflected by mirrors, and brought back together.

Now here’s the cool part. When a gravitational wave passes through, it slightly stretches one arm and compresses the other. The change is insanely small, smaller than the width of a proton. For reference, a proton is about 1.7 × 10⁻¹⁵ meters small! But that tiny difference changes how the laser beams recombine.

That change is recorded as data. LIGO is constantly collecting this data as a continuous stream over time. But here’s the problem, most of what it records is noise. Vibrations from the Earth, thermal effects, even distant human activity all get mixed in. The actual signal we care about is buried deep inside all that.

---

# What Came Before: Match Filtering

So how do we find a real signal in all that noise? This is where match filtering comes in.

Match Filtering is mainly a bunch of complicated math but to explain what is actually does, let us use an example.

Imagine you’re in a crowded room and a song is playing faintly in the background. If you already know the song, your brain can pick it out from the noise, regardless of all the other sounds in the room. You recognize the instruments used, beats it contains and the rhythm it follows.

Match filtering works in a similar way. Scientists generate thousands of possible templates, basically predictions of what a gravitational wave should look like for different kinds of events. Then LIGO’s data is scanned against all of these templates.

If something matches closely, there’s a good chance we’ve detected a real event.

---

# But recently… we’ve started doing something even better

Instead of manually comparing data to templates, what if a system could just learn what a signal looks like?

A newer approach called deep filtering uses machine learning models, especially neural networks, to automatically detect and analyze signals. Instead of relying only on predefined templates, these models are trained on huge amounts of simulated data. Over time, they learn to recognize patterns autonomously.

That means they can:
- Detect signals faster  
- Work better in noisy conditions  
- Extract features like mass and spin automatically  

In a way, instead of telling the system what to look for, we’re letting it figure things out by itself, and that’s what makes deep filtering so powerful.

---

## What’s happening under the hood?

Deep filtering essentially uses a stack of two 1D convolutional neural networks (CNNs) to process gravitational wave data.

Since LIGO data is a signal over time, not an image, we use a 1D CNN instead of the usual 2D one.

Think of the data as a long waveform. Now imagine a small window, called a kernel, sliding across that waveform. At each step, it looks at a small chunk of the data, learns patterns from it, and moves forward.

![alt text](assets/for_web/image.png)

Instead of trying to understand everything at once, the network breaks the problem into small parts, learns local features, and then combines them into a bigger understanding. Over time, it starts recognizing things like oscillations, spikes, and full waveform patterns that indicate real events.

---

### Why two networks?

Deep filtering uses two separate CNNs, each with a specific job.

**1. The Detector**  
The first network answers a simple question, "is there a signal here or not?" It scans incoming data and separates noise from potential gravitational wave signals. This step needs to be fast and reliable.


**2. The Predictor**  
Once a signal is detected, the second network takes over. Instead of just saying something is there, it tries to figure out what exactly happened. It extracts key features like the masses and other properties of the objects involved.

---

### Putting it together

So instead of manually comparing data to thousands of templates, deep filtering creates a pipeline:

- First, detect whether something interesting exists  
- Then, immediately analyze and extract meaningful information  

All of this can happen much faster, often in real time. It’s like having one system constantly listening for anything unusual, and another that instantly understands and explains what just happened.

---

## How do these networks actually learn?

Now comes the most interesting part: training.

At a high level, training is just a loop of:  
**see data → make a guess → measure error → improve**

---

### Step 1: Give it data (with answers)
You train these networks using simulated gravitational wave signals mixed with noise.
So the network sees:
- Pure noise  
- Noise with signals  
And for the predictor network, it also sees the correct physical parameters.


### Step 2: The network makes a guess
The data passes through all the layers.
At the beginning, everything is random, so the predictions are not great.

- The detector guesses signal or no signal  
- The predictor guesses properties like mass  


### Step 3: Measure how wrong it is
The output is compared with the correct answer.
This difference is called the loss. The bigger the loss, the worse the prediction.


### Step 4: Adjust the network
This is where learning happens. The network goes backward through its layers and adjusts each kernel slightly to reduce the error. If a pattern was missed, it learns to detect it. If it reacted to noise, it learns to ignore it.


### Step 5: Repeat
This process is repeated thousands of times.
Over time:
- Early layers learn simple patterns  
- Deeper layers learn complex waveform structures  


### Training the two networks
The two CNNs are usually trained separately:

- The detector learns to identify whether a signal exists  
- The predictor learns to estimate the properties of the signal  

Even though we talk about layers, you don’t train them one by one. The entire network learns together, automatically figuring out what each layer should focus on.

---