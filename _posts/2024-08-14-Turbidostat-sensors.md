---
title: 'Turbidostat: Optical density sensors'
date: 2024-08-14
permalink: /posts/2014/08/blog-post-3/
tags:
  - optics
  - spectrophotometry
  - adsorbance
---
Optical density (OD) describes the transmission of light through a highly blocking optical filter such that transmission ($$T$$) is very small. OD is mathematically expressed as the negative $$log_{10}(T)$$ where transmission is a physical value between 0 and 1.

$$
\displaylines{
OD = -log_{10}(T)
\\\
T=10^{-OD}
}
$$

<div align="center">
    <img src="/images/OD_drawing.png" >
</div>

Optical density measurements are crucial to measuring bacterial growth. These measurements are made by shooting light at a specific wavelength, typically 600 nm, through the test tube that the bacteria cannot absorb, but diffract and scatter resulting in decreased detectable transmission from an optical sensor on the other end of the tube. Naturally there should be a linear relationship between the amount of light blocked by the bacteria cells.

Cyanobacteria are photosynthetic and not only absorb light at most of the visible spectrum, but also release a photon in a phenomena called epifluoresence. Because I only have a simple light sensor that detects over a broad range of light, the chosen wavelength of light must not be in the photosynthetically active range. Hence the standard wavelength to measure cyanobacterial turbidity is 780 nm because it is near infrared and cannot be absorbed by photosynthetic pigments. I opted to use a 780 nm laser diode because simple LEDs have too broad of a wavelength distribution that bleed into the photosynthetic range. The optical sensor I chose is the [TSL2591](https://cdn-shop.adafruit.com/datasheets/TSL25911_Datasheet_EN_v1.pdf) from adafruit to make things easy for myself. It uses i2c addressing to control and comes with a nice [circuit_python](https://circuitpython.org/) library to make coding easy.

## Multiplexing sensors

<div style="float: left; margin-right: 20px; max-width: 30%;">
  <video style="width: 100%; height: auto;" controls>
    <source src="/images/multi_plex_TSL2951.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

Because the turbidostat will have at least 6 independent bioreactor vessels, I need to multiplex driving multiple TSL2951 devices. Because they use i2c addressing, I use the [TCA9548A](https://www.adafruit.com/product/2717) mutliplexor. If you are using circuit_python, you will want to use a microcontroller that uses a ATSAMD51 ARM processor due to issues with the TCA9548A library not compatible with other boards. I've linked 6 sensors together to a [M4 Metro Express Featherwing](https://www.adafruit.com/product/3857) from Adafruit. The board is connected to my laptop which is receiving a data stream through PySerial and writing the data to a csv file in realtime. This data is then plotted live using my custom [GUI](https://wongolini.github.io/posts/Turbidostat-UI/). The TCA9548A also supports daisy chaining so in the future I can have up to 21 sensors wired at the same time.


<br />
<br />


## Part List
- [M4 Metro Express Featherwing](https://www.adafruit.com/product/3857)
- [TSL2591](https://www.adafruit.com/product/1980)
- [TCA9548A](https://www.adafruit.com/product/2717)
- 780 nm laser diode

## Code Depedencies 
- Circuit Python and Circuit Python libraries
  - TSL2591
  - TCA9548A
 
- PySerial
- CustomTkinter
- Matplotlib
