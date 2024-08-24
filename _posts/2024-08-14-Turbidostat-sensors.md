---
title: 'Turbidostat: Optical density sensors'
date: 2024-08-14
permalink: /posts/2014/08/blog-post-3/
tags:
  - optics
  - spectrophotometry
  - adsorbance
---

Optical density measurements are crucial to measuring bacterial growth. These measurements are made by shooting a beam of light at a specific wavelength, typically OD600, that the bacteria cannot absorb, but diffract and scatter. This results in a decrease of light penetration as the light travels through the tube. The penetration of light is measured by a sensor, and the decrease in light detection compared against the bacterial density inside the tube. Naturally there should be a linear relationship between the amount of light blocked by the bacteria density and density of bacteria.

Cyanobacteria are photosynthetic and not only absorb light at most of the visible spectrum, but also release a photon in a phenomena called epifluoresence. This means choosing a wavelength of light in the visible spectrumn would not only be disrupted by absorbance, but also emission of a new photon at a different wavelength. Because I am using a simple photodiode sensor that does not filter a specific wavelength of light, I must choose a laser diode that shoots an near infrared 780 nm light beam since UV could photo-bleach or harm the cyanobacteria. The optical sensor I chose is the [TSL2951](https://cdn-shop.adafruit.com/datasheets/TSL25911_Datasheet_EN_v1.pdf) from adafruit to make things easy for myself. It uses i2c addressing to control and comes with a nice circuit_python library to make coding easy.


Uploading multi_plex_TSL2951.mp4…

