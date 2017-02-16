---
layout: page
title: DSP Library
permalink: /dsp/
---

### DSP Library
A basic collection of DSP code for the COSMO can be found in this [repository](https://github.com/cosmoproject/cosmo-dsp).

This repository comprises a library with [Audio Effects] (https://github.com/cosmoproject/cosmo-dsp/tree/master/DSP-Library/Effects) (e.g Reverbs, Delays, Distortion ..). If you have experience in writing Csound Patches, you can take one of the [examples] (https://github.com/cosmoproject/cosmo-dsp/tree/master/Examples) and modify them.

A better way to start building your effect instrument is using the [COSMO-Patcher] (https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher). Here you can define your instrument by simply assigning effect parameters to the harware controllers. A simple Patch looks like this:

    {"COSMO-Patch": {
        "pot0":
            {
                "Reverb": "Decay time",
                "Lowpass": "Cutoff frequency"
            },
        "pot1":
            {
                "Reverse": "Dry/wet mix"
            }
        }
    }
    
From this structure, the 'JsonToCsd.py' converter can generate the according Csound file. Find more instructions [here] (https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher).


![alt text](/images/Live_01.png "Live-01")

 We are planning to build a community sharing their individual csound-based effect instruments. If you'd like to share your code, [contact us](mailto:csoundonstage@gmail.com) and become added to the git-repository.
