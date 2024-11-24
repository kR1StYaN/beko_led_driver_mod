# meko_led_driver_mod

## FIRST OF ALL I AM NOT AN PROFESSIONAL. DO EVERYTHING AT YOUR OWN RISK.

## Introduction

I had an LED Driver (MEKO MKP035C1200BL) for light panels which used these cheap crappy remote controls. These remotes use a proprietary 2.4 ghz protocol and they communicate with an [TLSR8368E02EP16](https://wiki.telink-semi.cn/doc/ds/DS_TLSR8368-E_Datasheet%20for%20Telink%202.4GHz%20RF%20System-On-Chip%20Solution%20TLSR8368.pdf).

As i saw no possibility in emulating the remote and i wanted more control over the lights, i checked how the driver works. Luckily you can just pull out the driver, after you cut through the white stuff and pull out the driver sub board.
Luckily all pins are labeled here. It has 7 pins:
- Not Connected
- Warm White
- Cold White
- Blue
- Green
- Red
- Ground
- 3.3v

It seems like the driver is capable of doing RGB, but i did not test it and i don't know if the board is populated accordingly. My light just uses cwww.

All the channel links just output a PWM Signal at 3.3v and ~2000Hz. So you can just use an PWM Output from an ESP.

I used a Seed Studio C3 Supermini for this and created a custom LED Driver board. The code is inside of this repository. If you use different pins than me, be careful if the pins are involved in the boot process. Some pins are default high at boot and will cause the light to flicker when starting.
To connect my custom driver board, i used some legs of a capacitor. I could not find any matching pin headers on aliexpress. They have around 1.2mm pitch and 1mm pitch headers are too small.
After connecting everything and securing the pins with hotglue, i fired the light back on and could control it with esphome. 

## DON'T WORRY ABOUT LOUD COIL WHINE

You will encounter loud coil whining when the driver is turned on and the lights are not turned on. I checked with the normal driver, and it happens there also. If the cover is back on, you don't hear it as much.
