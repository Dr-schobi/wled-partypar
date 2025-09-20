\## WLED PartyPar



Modifying a cheap LED spot with WLED.



!\[modified PartyPar LED spot](outside.jpg)



Individually adressable LED strings seem to be everywhere and can easily be controlled with an ESP board and (Wled)\[https://kno.wled.ge/] firmware.

But for a quick temporary decoration the power supply, wiring and housing is not convenient.

For occasional decoration, I found an easy way to have an LED spot with adjustable color.



This Project is based on a \[https://www.thomann.de/de/fun\_generation\_usb\_partypar\_6\_rgb.htm](Thomann Fun Generation USB PartyPar) light. I got mine for 13,50€ each. But it comes in a plastic housing with a 5V 2A USB power supply and features 6x 3W RGB LEDs. Enough for a night-time Illumination or halloween decoration.



However, on its own, the light is dumb and can only blink.

I was able to modify the circuitry to be driven by an ESP32 which fits nicely into the housing and gives a seamless upgrade. For software, the \[https://kno.wled.ge/](WLED Project) directly supports setups with a single pixel and a PWM output. You get the benefit of wireless adjustments, multi-light synchronization and different animations.

It is surprisingly versatile for being just a single Pixel.





\### Credits



This work is inspired by \[https://protyposis.net/blog/rgb-led-party-spotlight-wled-upgrade/](protyposis) and based on the \[https://kno.wled.ge/](WLED Project). My contribution is minor and I just soldered 5 wires in the right place. 





\### Instructions

 

You need to open up the light and void the warranty (4 screws).

\[overview of the opened light](overview.jpg)



There is two PCBs inside, one PCB contains the LEDs and is screwed to the front housing.

I'm going after the Control PCB:

\[Original Control PCB](controlpcb.jpg)

We can find a microcontroller on the top right, the connector on the bottom right goes to the LED PCB.

The left side has three identical sections for driving each channel. 







I removed the built-in microcontroller to completely to disable the original functionality and added 5 wires (5V, GND, pwm\_R, pwm\_G, pwm\_B). Red and Black are GND and 5V for the ESP32 which conveniently go to J1.

The three channel PWM signals connect just like the control traces from the original microcontroller. I found that sodering to the resistor bank on the left seemedd convenient.



\[microcontroller removed and 5 wires added](withwires.jpg)



The wires also need to be soldered to the ESP. I usedd a pin header to disconnect for flashing firmware. The channel order could later be swapped in software. But make sure that your ESP32 is flashedd with WLED Firmware and is reachable. You might not be able to reach the connector ny more once fully assembled.

\[5 wires on the ESP32](wirestoesp.jpg)



Finally, the ESP32 needds to be fixed in the housing. I just hot-glued the module to the housing. With a just a dab of glue on the ESP shieldding, I have a chance of removing it later on.



\[internally assembled](assembled.jpg)





\### Software setup



The wled Firmware in the ESP32 needs to be set to one RGB-Pixel with PWM outputs.







\### drawback and alternatives



Well - these lights are limited in brightness and are useless other than night-time applications.

Higher powered LED fixtures exist and might still use PWM internally, but I could not find a good and cheap one.

Higher powered lights typically support DMX512.

I started with an WLED ESP32 to output DMX512 and also mount this directly into a light fixture.

Unfortunately, this requires re-compilation of wled and a few more wires. Stay tuned for more.







