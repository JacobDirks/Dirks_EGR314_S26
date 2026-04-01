---
title: API
---

<!--

Handling Code
You will next need to implement and expand the Message Protocol examples shared in class and available in the resources links above

Your job will be to:

Implement a message receiver that:
    handles all messages sent in over the daisy chain UART network
        passes on messages intended for someone else
        processes messages intended for you.
        trashes messages sent from yourself that have made it back to you
        ignores messages larger than your buffer size
    anticipates and handles mal-formed messages by ignoring them. For example:
        ignores characters sent outside of a message frame
    handles each message type intended for you
        must provide a unique acknowledgement of the message and the data received, whenever a correctly-formatted message is received.
        This does not have to connect to your final system functionality yet, but should be differentiable based on the message type and message data received

Implement a message sender that
    sends an example of each message type, properly formatted, with time-varying data (can be valid data or "dummy" data for now).
        easily modifiable based on the instructor's request (see below)
    ensures that data you send is properly formatted
        contains proper prefix and suffix
        is properly addressed by you, and properly addressed to someone on your team.
        ensures that message data does not contain message prefix and suffix codes.
        cannot send data that is longer than the specification.
        any other other reasonable formatting mistakes are prevented.
        prioritizes passing on messages received by you before sending your own messages.
        ensures a maximum rate of sending messages determined by a specified variable, and implemented using programming best practices, such as interrupts, timers, and non-blocking code.

 -->
<!--
 Messages intended for me to act on something

 Messages at me
| Message Num | Byte 1-2(uint16_t) | Byte 3 (uint8_t) | Byte 4 (uint8_t) | Byte 5 (uint8_t) | Byte 6 (uint8_t) | Byte 7 (uint8_t) | Byte 8 (uint8_t) | Message Reason |
| 1 | 0x01 | Subsystem number | Motor number | Upper number | Lower number | String Space | String Space | Set Motor to a certain parameter |
| 12 | 0x0C | Subsystem number | Upper number | Lower number | String Space | String Space | String Space | Get Subsystem status |
-->

The only messages that will be directed to me are ones from the submarine's controller interface and are denotated by being sent through subsystem 2. However below each message chart I put a translated byte message.

|  Individual | No. |
| :------: | :------: |
|  Sam B      |  1  |
|  Adrian P   |  2  |
|  Andrew I   |  3  |
|  Jacob D    |  4  |
|  Sam M      |  5  |
|  Mo A       |  6  |

## **Messages Directed To The Motor Subsystem**

**Message Type 1 -- Motor Speed Set Message**

|               |    Byte 1    |      Byte 2      |  Byte 3  |    Byte 4   |     Byte 5     |   Byte 6     |
|  :----------: | :----------: |   :----------:   | :----------: | :----------: | :----------: | :----------: |
| Variable Name | message_type | subsystem_Number | motor_Id | Upper motor_Speed |  Lower Motor Speed | motor_Direction|
| Variable Type |    uint8_t   |     uint8_t      |  uint8_t |   int8_t    |     int8_t     |       int8_t |
|   Min Value   |      1       |       4          |    1     |     0       |        0       |            0 |
|   Max Value   |      1       |       4          |    2     |    15       |        15      |            1 |
|    Example    |      1       |       4          |    1     |    4        |        4       |            1 |

Example: 415A241414415942

**Message Type 12 -- Request Subsystem Status**

<!-- Not sure what else should be here-->

|   Column name |     Byte 1    |      Byte 2      | Byte 3 |
| :----------: | :----------: | :----------: | :----------: |
| Variable Name |  message_type | subsystem_Number |  code  |
| Variable Type |     uint8_t   |     uint8_t      | uint8_t |
|   Min Value   |      12       |       4          |  0     |
|   Max Value   |      12       |       4          |  15    |
|    Example    |      12       |       4          |  3     |

Example: 415A24C435942

<!--
 Messages I send
| Message Num | Byte 1-2(uint16_t) | Byte 3 (uint8_t) | Byte 4 (uint8_t) | Byte 5 (uint8_t) | Byte 6 (uint8_t) | Byte 7 (uint8_t) | Byte 8 (uint8_t) | Message Reason |
| 2 | 0x02 | Subsystem number | Motor number | Upper number | Lower number | String Space | String Space | Print out the motor Information
| 10 | 0x0A | Subsystem number | Upper number | Lower number | String Space | String Space | String Space | Print error in subsystem |
| 13 | 0x0D | Subsystem number | String Space | String Space | String Space | String Space | String Space | Print out subsystem status
-->

## **Messages Sent By the Motor Subsystem**

**Message Type 2 - Alert Control Unit of Motor Information**

|               |    Byte 1    |      Byte 2      |  Byte 3  |    Byte 4   |     Byte 5     | Byte 6 |
| :----------: | :----------: | :----------: | :----------: | :----------: | :----------: | :----------: |
| Variable Name | message_type | subsystem_Number | motor_Id | Upper motor_Speed |  Lower Motor Speed | motor_Direction|
| Variable Type |    uint8_t   |     uint8_t      |  uint8_t |   int8_t    |     int8_t     |       int 8_t  |
|   Min Value   |      2       |       2          |    1     |     0       |        0       |         0      |
|   Max Value   |      2       |       2          |    2     |     15      |        15      |      1       |
|    Example    |      2       |       2          |    1     |      4      |        0       |        0        |

Example: 415A422214005942

**Message Type 14 - Alert Control Unit to Subsystem Error**

|               |    Byte 1    |      Byte 2      |  Byte 3    |    Byte 4   |
| :----------: | :----------: | :----------: | :----------: | :----------: |
| Variable Name | message_type | subsystem_Number | Error_Code |  sender_Num |
| Variable Type |    uint8_t   |     uint8_t      | int8_t     | uint8_t     |
|   Min Value   |      10      |       2          |  0         |      4      |
|   Max Value   |      10      |       2          |   64       |      4      |
|    Example    |      10      |       2          |    10      |      4      |

Example: 415A42A2A45942

**Message Type 15 - Alert Control to Subsystem Status**

|               |    Byte 1    |      Byte 2      |  Byte 3    |    Byte 4   |
| :----------: | :----------: | :----------: | :----------:   | :----------: |
| Variable Name | message_type | subsystem_Number | sender_Num | status_Code |
| Variable Type |    uint8_t   |     uint8_t      |   uint8_t  |  int8_t     |
|   Min Value   |      13      |       2          |      4     |       0     |
|   Max Value   |      13      |       2          |      4     |      10     |
|    Example    |      13      |       2          |      4     |       5     |

<!-- All codes will start with 0x415A and end with 0x5942-->
Example: 415A42D2455942

All of this documentation can be found in this ["Project Code Zip File"]() for your replication and viewing leisure.
