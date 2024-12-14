## Introduction   

Based on project 02, I decided to add some communication elements. In the test of the previous project, I found that people have difficulty reading the answers of the Ouija board.
So, this is a small metaphysical experience. Users can first silently recite the questions they want to answer, then move the small triangle on the Ouija board, wait for the Ouija board to show the answer, open the locked box after the answer is shown, take out the answer decryption book from it, crack the code, and get the answer

## Implementation   

I divided the whole process into two steps
First I tried to solve the problem of two hardwares communicating. At first, I chose to use wifi for communication between the two hardwares
``` Python  
if(sensor_val > 100):  # sensor value higher than threshold
   led_pin.on()  # turn on LED
```

Then I made a small box with the answer code book out of cardboard
After obtaining the data, I drew a drawing for the laser
![state diagram example](IMG_9192.jpeg)  

Then I went to laser print the assembly parts of the small box
![state diagram example](IMG_9222.jpeg)  

### Hardware

* Atoms3-lite
* Extended Dupont Cables
* 360 Motors

![state diagram example](IMG_2474.PNG)  

### Firmware   

Provide a link to your MicroPython code and explain the important parts that make your prototype work.  Most likely you should explain the inputs/outputs used in your code and how they affect the behavior of the prototype.

To include code snippets, you can use the code block markdown, like this:

``` Python  
if(sensor_val > 100):  # sensor value higher than threshold
   led_pin.on()  # turn on LED
```

### Software   

If applicable, explain the important software components of your project with relevant code snippets and links.  

### Integrations   

Include a link to and/or screenshots of any communication components used in your project, like Adafruit IO feeds, dashboards, IFTTT applets, etc.  

### Enclosure / Mechanical Design   

Explain how you made the enclosure or any other physical or mechanical aspects of your project with photos, screenshots of relevant files such as laser-cut patterns, 3D models, etc. (it’s great if you’re willing to share the editable source files too!)

## Project outcome  

Summarize the results of your final project implementation and include some photos of the prototype and a video walkthrough showing it working.  

Note that GitHub has a small size limit for uploading files via browswer (25Mb max), so you may choose to use a link to YouTube, Google Drive, or another external site.

## Conclusion  

As you wrap up the project, reflect on your experience of creating it.  Use this as an opportunity to mention any discoveries or challenges you came across along the way.  If there is anything you would have done differently, or have a chance to continue the project development given more time or resources, it’s a good way to conclude this section.

## Project references  

Please include links to any online resources like videos or tutorials that you may have found helpful in your process of implementing the prototype. If you used any substantial code from an online resource, make sure to credit the author(s) or sources.  
