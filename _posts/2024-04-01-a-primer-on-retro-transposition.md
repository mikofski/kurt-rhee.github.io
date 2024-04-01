---
layout: post
title: A Primer on Retro-Transposition
description: Blog
summary: A Primer on Retro-Transposition
tags: [transposition, retro-transposition, pyranometer, plane of array]
---


![Flat]({{ site.url }}/assets/images/solar-panels-retrotransposition.jpeg#center)
**Figure 2:**  A rendition of a light hitting some solar panels generated by Gemini

# Introduction

Photovoltaic performance models which can accept plane of array irradiance (POAI) or global transposed irradiance (GTI) do not use the
input POAI data directly.  Instead, the POAI is "retro-transposed" into horizontal components (GHI, DHI, DNI) and then re-transposed into the plane of array.  Some may wonder, why go through this extra series of steps if the POAI data is readily available? 

# Primer

The main reason for retro-transposing the POAI is that measured POAI does not contain the irradiance components (diffuse irradiance in the plane of array and direct irradiance in the plane of array) needed for some of the models in the performance model chain.  These values are necessary in order to determine what portion of irradiance is lossed due to:

    1. The incidence angle effects in the glass which has both a direct component (1) and a diffuse component (2).
    2. The shade loss which also has a direct (3) and diffuse (4) component.

Mounting pyranometers in the plane of array configuration is a popular way of reducing the uncertainty introduced by transposition models, but introduces a few uncertainties of its own.  For example:

- The plane of array pyranometer on a tracker system may not be aat the correct rotation angle if the tracker goes offline.
- Tracker systems which have different rotation algorithms for individual trackers (3) will not be correct due to the different rotation angles.
- The mounting of the plane of array pyranometer may be influenced by direct or diffuse shading, which would cause the performance model to double count the loss.
- Uncertianty in the retro-transposition model can incorrectly estimate the proportion of diffuse and direct irradiance in the plane of array.
- PV Performance modeling software can possibly use a different retro-transposition algorithm than the transposition algorithm which introduces confusion.  
- If the retro-transposition algorithm allocates the circumsolar portion of irradiance to diffuse and then the transposition algorithm allocates the circumsolar portion of irradiance to direct, the resulting energy model effects are entirely unstudied.

Because of these uncertainties (especially the first three), plane of array pyranometers should be treated with extra caution when evaluating operational data.  It is my opinion that tracked utility scale PV power plants should have at least 2 pyranometers in the horizontal configuration to fall back on for periods when the plane of array pyranometers are not giving good data.  I also believe that diligently siting pyranometers to avoid diffuse and direct shading is important for all utility scale powerplants. 

# Conclusion

Retro-transposition is an often overlooked portion of the PV performance model

**Further reading:** 
- [GTI Driesse](https://www.sciencedirect.com/science/article/pii/S0038092X23007272)
- [PVPMC Effective Irradiance](https://pvpmc.sandia.gov/modeling-guide/2-dc-module-iv/effective-irradiance/)
- [(1) Physical IAM](https://pvlib-python.readthedocs.io/en/v0.9.0/generated/pvlib.iam.physical.html)
- [(2) Marion Diffuse](https://pvlib-python.readthedocs.io/en/v0.9.0/generated/pvlib.iam.marion_diffuse.html)
- [(3) Direct Shading](https://kurt-rhee.github.io/2024/01/19/a-physical-shade-shape-calculation-algorithm)
- [(4) Diffuse Shading](https://pvlib-python.readthedocs.io/en/stable/gallery/shading/plot_passias_diffuse_shading.html)
