---
title: Hardware V2.0
---

## **Version 2 Updates**

Since this is only a semester long project there isn't time to do a full build cycle and then start over and work on a final copy. Therefore, lots of the boards end up with jumper wires or simple fixes. This is obviously unideal and leads to a significant number of changes that could be made. Therefore, without further ado here's the bare bones list.

    * More test points
    * Spread out regulators from other components
    * Don't ground pmd, dis, dir pins on the motor controller permanently
    * Add jumper pins ( no really it would've saved a LOT of time )
    * Utilizes the back of a board as well for parts
    * Decrease Via's on the board as a whole.
    * Build a stand system into the board
    * ESD (Electrostatic Discharge) Protection

Now why would someone want more test points? First they can be replaced by male pin headers or become a spot for soldering on new connections which makes it significantly better for hot fixing elements. Secondly, test points are **test** points and can be used to check electrical signals. This slightly goes in line with the jumper pins because jumper pins can also be used as a test point. However, jumper pins are also really nice because they can be used to cut off signals to high risk areas or isolate a power to ground connection point without de-soldering half the board. Space also became a significant issue to the point where I had to pull a regulator off the board entirely because I wouldn't have been able to get its replacement back onto the board with my skill level at the time. That skill level has since changed due to the amount of tight solder positions as well as experience with more surface mount components. Otherwise the next big element is using the back of the board because that was free real estate and would have helped **significantly** reduce the tight corners and partially melted plastic housings because the iron had a larger clearance than I planned for. By using the back of the board one might think that I would have more via's but currently I have to jump signals over each other so there are a lot of vias that would otherwise be removed. Also by adding parts onto the bottom/back of the board a quality of life update would be to add a stand for the board so I wouldn't be working on top of components. This would also help with the lab situation as 10 teams composed of 58 students total all worked within the same lab. Finally, arguably the most important hardware change would be, adding electrostatic discharge protection around my ESP32 - S3 chip. I had to de-solder and re-solder that chip enough times that I got annoyed looking at it. Sometimes it was from too much current or a backlash of it causing a problem. Other times the ESP decided it had a rough day and would stop working in between testing days. 
