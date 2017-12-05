# I2S_parallel_example_drive_a_64x32_display
I2S parallel example drive a 64x32 RGB display. 

# Read more about this example 
https://esp32.com/viewtopic.php?f=17&t=3188#p14940

# Taken from the origin Post (ESP_Sprite):
So while we're still working on some kind of official driver for the parallel mode of the I2S peripheral, we do already have some logic for it working. Essentially, we can use DMA to set up a round-robin buffer to output a selected set of buffers over and over again. THis is ideal for generating a fixed signal of some sorts, and can be used to control a 'dumb' LED-display. 

This is what we did:
![testanimation](https://raw.githubusercontent.com/ESP32DE/I2S_parallel_example_drive_a_64x32_display/master/output.gif)

The logic involved actually is somewhat more involved than it may look: because the LEDs on the screen can only lit on 2 out of the 16 rows at the time, the display needs to be continuously supplied with data. To complicate things even more, each subpixel can only be turned off or on, so there's no chance of doing grayscale... unless you send a bazillion subframes to get something like PWM working. The end result is that the DMA engine in the ESP32 is put to good use here, continuously pumping about 100MBit of data into the LED-display without using up a single percent of CPU power. 

The result is pretty good:
![testpic](https://raw.githubusercontent.com/ESP32DE/I2S_parallel_example_drive_a_64x32_display/master/20170930_114830_s.jpg)

Be aware that this is preliminary work and it comes with no guarantees or support from Espressif.

  
 
