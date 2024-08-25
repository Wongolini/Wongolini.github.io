---
title: 'Turbidostat: Optical density sensors'
date: 2024-08-14
permalink: /posts/2014/08/blog-post-3/
tags:
  - optics
  - spectrophotometry
  - adsorbance
---
Optical density (OD) describes the transmission of light through a highly blocking optical filter such that transmission ($T$) is very small. OD is mathematically expressed as the negative $log_{10}(T)$ where transmission is a physical value between 0 and 1.

$$
\displaylines{
OD = -log_{10}(T)
\\\
T=10^{-OD}
}
$$

Optical density measurements are crucial to measuring bacterial growth. These measurements are made by shooting light at a specific wavelength, typically 600 nm, that the bacteria cannot absorb, but diffract and scatter resulting in decreased transmission. The transmission is measured by a sensor, and the decrease in light detection compared against the bacterial density inside the tube. Naturally there should be a linear relationship between the amount of light blocked by the bacteria density and density of bacteria.

Cyanobacteria are photosynthetic and not only absorb light at most of the visible spectrum, but also release a photon in a phenomena called epifluoresence. This means choosing a wavelength of light in the visible spectrumn would not only be disrupted by absorbance, but also emission of a new photon at a different wavelength. Because I am using a simple photodiode sensor that does not filter a specific wavelength of light, I must choose a laser diode that shoots an near infrared 780 nm light beam since UV could photo-bleach or harm the cyanobacteria. The optical sensor I chose is the [TSL2951](https://cdn-shop.adafruit.com/datasheets/TSL25911_Datasheet_EN_v1.pdf) from adafruit to make things easy for myself. It uses i2c addressing to control and comes with a nice [circuit_python](https://circuitpython.org/) library to make coding easy.

## Multiplexing sensors

<div style="float: left; margin-right: 20px; max-width: 30%;">
  <video style="width: 100%; height: auto;" controls>
    <source src="/images/multi_plex_TSL2951.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

Because the turbidostat will have at least 6 independent bioreactor vessels, I need to multiplex driving multiple TSL2951 devices. Because they use i2c addressing, I use the [TCA9548A](https://www.adafruit.com/product/2717) mutliplexor. If you are using circuit_python, you will want to use a microcontroller that uses a ATSAMD51 ARM processor due to issues with the TCA9548A library not compatible with other boards. I've linked 6 sensors together to a [M4 Metro Express Featherwing](https://www.adafruit.com/product/3857) from Adafruit. The board is connected to my laptop which is receiving a data stream through PySerial and writing the data to a csv file in realtime. This data is then plotted live using my custom [GUI](https://wongolini.github.io/posts/Turbidostat-UI/) 



<br />
<br />


## Part List
- [M4 Metro Express Featherwing](https://www.adafruit.com/product/3857)
- [TSL2951](https://www.adafruit.com/product/1980)
- [TCA9548A](https://www.adafruit.com/product/2717)
- 780 nm laser diode

## Code Depedencies 
- Circuit Python and Circuit Python libraries
  - TSL2951
  - TCA9548A
 
- PySerial
- CustomTkinter
- Matplotlib
