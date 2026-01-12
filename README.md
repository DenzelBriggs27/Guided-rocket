# Guided-rocket
Project submission for an aerodynamically controlled rocket, with active stabilization achieved by aft fin control. The fins are controlled by a custom-made PCB based around the STM32f446RET6 MCU.
The goal of this rocket is to stabilize trajectory on the roll, pitch, and yaw, axes by deflecting the aft fins of the rocket, producing controlled side forces. This project will incorporate CFD, filters, and control systems to achieve this goal. 

This project is a step in my pursuit of a career in aerospace, granting me new knowledge in various areas. 

CAD:
<img width="1470" height="956" alt="Screenshot 2025-12-11 at 12 46 26 PM" src="https://github.com/user-attachments/assets/a4ba7400-3c0a-4794-9abe-f25e5b22ca4e" />

There were tons of updates and small changes made periodically, so I'm just going to show the finished product and do a general description of the process and mechanics.

<img width="1470" height="956" alt="Screenshot 2025-12-11 at 9 12 27 AM" src="https://github.com/user-attachments/assets/e8bf04ac-a75a-4c32-a136-808fed0b426f" />

This rocket is meant to fly on the 29mm G80t motor, which doesn't leave much room in the aft section for much, so I had to get creative with a servo linkage to the fins with a custom-made horn. The fins are connected to a connector which allows them to slot into a small circular bearing.

<img width="1470" height="956" alt="Screenshot 2025-12-11 at 12 00 54 PM" src="https://github.com/user-attachments/assets/3a8f7deb-4acd-4389-bf0d-1baa82fb5907" />
The servos are controlled by a pcb near the aft of the rocket

<img width="1470" height="956" alt="Screenshot 2025-12-11 at 12 01 56 PM" src="https://github.com/user-attachments/assets/86342cd3-866d-4ed6-b688-589d570a14a7" />
<img width="1470" height="956" alt="Screenshot 2025-12-11 at 12 03 56 PM" src="https://github.com/user-attachments/assets/b80ec63f-7348-40eb-ae1d-09a9b25ad866" />
The parabay will hold the parachute and will separate after apogee, a raceway cable will travel along the side of the interior, containing the servos power and pwm wires.

<img width="1470" height="956" alt="Screenshot 2025-12-11 at 12 10 56 PM" src="https://github.com/user-attachments/assets/c1e495e7-7b4d-4a26-a576-d5c8fba7f44e" />
Above the parabay is the lipo housing and avionics bay, the whole vehicle is powered by a 7.4v 2600mAh battery, supplying to the servos and flight computer. The avionics bay consists of my primary custom flight controller, a radio, and a microsd card breakout board for telemetry and flight data logging respectively.

<img width="1920" height="1080" alt="Untitled design (3)" src="https://github.com/user-attachments/assets/c278681d-da3c-4d22-bd47-ac5ea40d89a6" />
The ellipsoidal nose cone contains an esp32 s3 module with an ov2640 cam, this allows not only for footage, but for bluetooth and wifi capabilities, allowing setup processes such as fin actuation tests to be run from a phone.


PCB:
<img width="559" height="785" alt="Screenshot 2025-12-12 at 4 37 38 PM" src="https://github.com/user-attachments/assets/913f469d-e7c6-45af-949c-ed1152d5d8db" />
<img width="469" height="826" alt="Screenshot 2025-12-12 at 4 47 43 PM" src="https://github.com/user-attachments/assets/c0971dd9-6928-4bb9-987b-3680372c4987" />
I designed a custom PCB for telemetry and guidance calculations, centered around a STM32f446RET6 MCU, and powered by a 7.4v LiPo battery. It has 3 IMUS: BMI088, H3LIS331DL, and a BNO085. These IMUs were chosen for their different G ranges, their data will be integrated into a Kalman filter, then used to calculate the correct fin deflection angle to correct the rocket's orientation. The board also has a SAM-M10q-00b GNSS receiver, a bmp390 altimeter, 2 pyro charges with continuity detection, 4 pwm outputs, an SPI output, and a UART output for telemetry with an XBee 900hp over the 900 mHz band. This radio link allows for commands to be sent by the ground center, for which I designed a slightly different PCB:


<img width="729" height="699" alt="Screenshot 2025-12-11 at 1 38 38 PM" src="https://github.com/user-attachments/assets/90a869da-5065-46ff-ae69-0e4e04beb4ff" />
<img width="1470" height="956" alt="Screenshot 2025-12-11 at 1 39 33 PM" src="https://github.com/user-attachments/assets/9d9a0edd-549d-4ef0-af54-124ff40e6f22" />
This PCB and a second xbee900hp allows for a radio datalink between the rocket and ground station, with a maximum range of ~28 miles. Over this radio datalink, telemetry (orientation, position, velocity, acceleration) and commands (fin tests, flight presets) will be sent.


Thanks for viewing my project!
