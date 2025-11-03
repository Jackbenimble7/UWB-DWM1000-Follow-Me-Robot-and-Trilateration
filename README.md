# UWB-DWM1000-Follow-Me-Robot-and-Trilateration
A real-world UWB ‘follow-me’ system using ESP32 + DW1000 modules for a DIY golf push cart. Includes anchor and tag firmware, ESP-NOW communication, trilateration, field calibration, and lessons learned from outdoor testing. This repository can be utilized for any type of following robot.


# Overview
I have seen many online repositories, blog posts, and forum questions around both the DWM1000 UWB module and a more general "follow-me" robot concept. All of these resources were useful in their own right, but I didn't come across excatly what I was looking for, which was to create a following robot using some sort of sensor paired with an ESP32. So I wanted to create this repository to help others who are trying to figure out how to make a robot or any wheeled object follow them. My application pertains specifically to a remote control golf push cart. I built my push cart using hoverboard motors and it worked really well, but I wanted to find a good way to make my golf cart follow me when I'm out on the course. This repository should be helpful to people trying to make ANY type of following device, not just a golf cart. 

# Background
To start, I had 
