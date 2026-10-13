---
title: "Do Deepfakes have a heart?"
date: "2026-10-13"
---
While looking for interesting papers to reccommend to one of my friends I came across this paper which makes the bold claim that we can detect deepfake by using a Computer Vision technique to detectet if the person in the video has a pulse! lets talk about this

## rPPG
This idea, Remote photoplethysmography (rPPG), initaly made for the medical field uses Computer Vision models(varies for different implementation)  to try  finding  pulse/heartbeat of a person thorugh video

Now before i get into how it does this, lets talk about how is this usefull for Deepfake detection.

Deepfake is basicaly when AI models are used to make "fake faces" or face swaps (putting face of oner person in body of other). The AI gen videos of famous people you see on instgram reels or yt shorts is a good example of it.

Every human has a pulse (living ones atleast), and AI models cannot replicate this pulse cause they dont exist. Hence If we could detect these pulses and if a video has no detetcable pulse we can say its deepfake

## How is this done?
good question reader!

regardless of the model stack, the main method is that the cv models observes the left and right cheek of the person, the cheeks have a good blood supply and are usualy well exposed from most angles where the face is visible. The Model then looks for periodic fluctuations in the green wavelgeth .

Why green? Well green light is absorbed strongly by blood, so small heartbeat changes in blood volume create relatively clear changes in the skin’s reflected green light also camera's sensors also tend to capture green well.

These periooic changes after being detected are fed forward into the model where it assigns a confidence score of whether the changes detected are similar to a pulse and helps give a confiedce rating to the detction mechanism 

## How to actualy implemet this 
several papers have different methods of doing this , 
["one paper reccomends a using CNN feeding into a LSTM model"](https://www.sciencedirect.com/science/article/pii/S2665910726000617)
![](/content/til/image.png)


["another paper implents a CNN feeding into a MLA and Transformer model "](https://link.springer.com/article/10.1007/s00371-023-02833-x)
![](/content/til/image-1.png)

## Limitations
Earlier when i said deepfake cant make pulses, i was not showing the enitre picture(apologies). High quality deepfakes infact can replicate pulses to try and foo rPPG sensors like these. This also brings up another issue. 

rPPG based Deepfake detectors are bad adt dettecing face swaps, a limitation mentioned in several papers, regardless a very cool application of Computer vision + medtech.
