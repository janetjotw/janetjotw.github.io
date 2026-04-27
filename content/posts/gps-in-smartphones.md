---
title: "GPS in Smartphones"
date: 2022-08-15T13:38:43+00:00
draft: false
---

Have you ever wondered how the Maps load on your smartphone? You might even know that it is GPS that helps with the navigation and be able to share your coordinates with a friend to meet at a common point. But how does GPS really work? I hope to cover this with some explanation.

## What is GPS?

GPS stands for **G**lobal **P**ositioning **S**ystem and is a type of global navigation satellite system (GNSS). It is a satellite based navigation system made up of a network of 24 satellites placed into orbit. It is a technology developed by the United States Department of Defense.

## How does GPS work?

GPS satellites circle the earth in the orbit and transmit signals into the earth. The satellites have multiple atomic clocks synchronized with Coordinated Universal Time (UTC) and broadcast signals in the gigahertz (GHz) range. Modern smartphones have a GNSS receiver. The receiver captures the radio signals and decodes them. The time can be compared to see when the signal was transmitted by the satellite and the timestamp when it was received on the receiver. This is also referred to as GPS clock synchronization. Wireless networks and data networks use the GPS timing to keep the cellular base stations in sync.

![](/images/gps-in-smartphones/janet-gps-1.png)

GNSS receivers are implemented on a single chipset that supports single frequency operation on a single electronic integrated circuit (IC). The terms chip, microchip, IC, and silicon chip are synonymous. A chip can function as an entire computer that resides on a device having RAM, ROM, clock, the input and output control unit and CPU. GNSS receivers have 2 parts--antenna and the processing unit.

The basic block diagram shows a high-level overview of the components on a smartphone. The diagram will not focus on the external components typically seen on an IC. The aim is to illustrate how the GNSS receiver is integrated onto a circuit.

![](/images/gps-in-smartphones/gnssrec-1.png)

## Location Positioning 

Raw measurements from the GNSS receiver helps in the calculation of location. To calculate position, signal propagation from 4 satellites are determined. These signals are translated into the geo-coordinates that are computed as latitude (lat), longitude (long), altitude, and time. The lat and long coordinates help with precise positioning which is used in various use cases today.

## Alternatives to GPS

The greater the signal strength, the reception quality is better. The GNSS signals are weaker when there are obstructions. The receiver must get a clear line of sight view for location determination. If you are inside a building or a parking lot, the visibility to satellites is impaired. GPS is precise most times for outdoors. But it is a drain on the battery, not effective for long-term use, and does not work indoors. So smartphones today have come up with alternatives like A-GPS (Assisted GPS) or WiFi networks. A-GPS makes use of the cellular towers for positioning. In many scenarios, especially with regards to accuracy, it would require a combination of multiple technologies also termed as hybrid including GNSS based solutions, radio-technologies (e.g. LTE networks, Wi-Fi networks, beacons etc.). 

GPS is used in the US, but it is not the same satellites globally used around the world. The other global GNSS systems are--GLONASS (Russia), Galileo (EU), BeiDou (China). Additionally, there are two other regional systems--QZSS (Japan) and IRNSS or NavIC (India).