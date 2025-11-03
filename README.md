# UWB-DWM1000-Follow-Me-Robot-and-Trilateration
A real-world UWB ‘follow-me’ system using ESP32 + DW1000 modules for a DIY golf push cart. Includes anchor and tag firmware, ESP-NOW communication, trilateration, field calibration, and lessons learned from outdoor testing. This repository can be utilized for any type of following robot.


# Overview
I have seen many online repositories, blog posts, and forum questions around both the DWM1000 UWB module and a more general "follow-me" robot concept. All of these resources were useful in their own right, but I didn't come across excatly what I was looking for, which was to create a following robot using some sort of sensor paired with an ESP32. So I wanted to create this repository to help others who are trying to figure out how to make a robot or any wheeled object follow them. My application pertains specifically to a remote control golf push cart. I built my push cart using hoverboard motors and it worked really well, but I wanted to find a good way to make my golf cart follow me when I'm out on the course. This repository should be helpful to people trying to make ANY type of following device, not just a golf cart. 

# Background
To start, I tried figuring out the best way to create a follow-me mode. I basically wanted something that I could connect to my ESP32 on my golf cart that would follow some sort of beacon that I held in my pocket. I worked through the following options and discarded them for the following reasons. 

Bluetooth

The way this would have worked would be to use either my phone or a battery powered ESP32 in my pocket to send out bluetooth signals to the ESP32 located on the golf cart. The golf cart ESP32 would register the strength of the Bluetooth signal and use that to determine how far away it was from the "beacon." You could mount two ESP32s on the robot, one on the left and one on the right, and use trilaterization to figure out the x and y coordinates of the beacon. This is something that could work, however Bluetooth is extremely noisy and signal strength is not a very reliable measurement. In a pinch, I think this option could work, but I wanted something that would be more accurate. 

ESP-NOW Signals

Same idea as above. The ESP32 beacon sends ESP-NOW signals to the cart-mounted ESP32s. The cart-mounted ESP32s use signal strength to determine x and y coordinates. Again, this is unreliable and not very accurate. 

GPS

I looked extensively into GPS, but unfortunately, the standard GPS sensors are only accurate to within 3 to 5 meters. This is not very useful when I want my cart to start following me when it is 5' behind me and stop when it is also 5' behind me. There are more advanced versions of GPS (RTK) but these are expensive and complicated. I think GPS COULD work if you were in a wide-open area with good satelite access, but again, I wanted something more accurate and robust. 

Ultrasonic Sensors

This could work and I at first tried experimenting with it based on this blog post: https://elliotmade.com/2022/05/04/ultrasonic-direction-and-range-finding-hack/
However, I could not for the life of me figure out how to get these modified ultrasonic sensors to work, so I ended up shelving the project. Either way, these sensors also have major limitations in that they are really only good for up to around 4m (12') and even that can be dicey. They are just not accurate enough for the following process I wanted. They also require having an ultrasonic sensor on your person pointed directly at the ultrasonic sensors mounted on the golf cart. Sure, you could clip a ultrasonic sensor pointed backwards on your belt, but it's going to be extremely unreliable. 

IR Sensors

Similar issues as ultrasonic sensors. Even worse in that light degrades the signal strength very quickly. 

LIDAR

Not really a good option for following. It is good at giving you distances to objects, but it doesn't "communicate" between anchors and beacons, so to speak. 

Ultimately, after doing a lot of research, I stumbled across ultra-wideband (UWB) technology and specifically, the DWM1000 chip. This chip gives you precise distance measurements down to 10cm in accuracy and the module itself only costs ~$25. Even though this is a more complicated sensor than some of the others, this seemed to be the right fit for my application. 
