---
title: API
---

<!--
 Messages intended for me to act on something

 Messages at me
| Message Num | Byte 1-2(uint16_t) | Byte 3 (uint8_t) | Byte 4 (uint8_t) | Byte 5 (uint8_t) | Byte 6 (uint8_t) | Byte 7 (uint8_t) | Byte 8 (uint8_t) | Message Reason |
| 1 | 0x01 | Subsystem number | Motor number | Upper number | Lower number | String Space | String Space | Set Motor to a certain parameter |
| 12 | 0x0C | Subsystem number | Upper number | Lower number | String Space | String Space | String Space | Get Subsystem status |
-->

The only messages that will be directed to me are ones from the submarine's controller interface and are denoted by being sent through subsystem 2. However below each message chart I put a translated byte message. With that said each message will start with AZ + Sender Code + Desired Recipient Code before the message. After the body of the message is sent the end is always BY as a way to ensure that value acts as the clear and decisive end.

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

Example: AZ14141441

**Message Type 12 -- Request Subsystem Status**

<!-- Not sure what else should be here-->

|   Column name |     Byte 1    |      Byte 2      | Byte 3 |
| :----------: | :----------: | :----------: | :----------: |
| Variable Name |  message_type | subsystem_Number |  code  |
| Variable Type |     uint8_t   |     uint8_t      | uint8_t |
|   Min Value   |      12       |       4          |  0     |
|   Max Value   |      12       |       4          |  15    |
|    Example    |      12       |       4          |  3     |

Example: AZ141243

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

Example: AZ41221400

**Message Type 14 - Alert Control Unit to Subsystem Error**

|               |    Byte 1    |      Byte 2      |  Byte 3    |    Byte 4   |
| :----------: | :----------: | :----------: | :----------: | :----------: |
| Variable Name | message_type | subsystem_Number | Error_Code |  sender_Num |
| Variable Type |    uint8_t   |     uint8_t      | int8_t     | uint8_t     |
|   Min Value   |      10      |       2          |  0         |      4      |
|   Max Value   |      10      |       2          |   64       |      4      |
|    Example    |      10      |       2          |    10      |      4      |

Example: AZ41102104BY

**Message Type 15 - Alert Control to Subsystem Status**

|               |    Byte 1    |      Byte 2      |  Byte 3    |    Byte 4   |
| :----------: | :----------: | :----------: | :----------:   | :----------: |
| Variable Name | message_type | subsystem_Number | sender_Num | status_Code |
| Variable Type |    uint8_t   |     uint8_t      |   uint8_t  |  int8_t     |
|   Min Value   |      13      |       2          |      4     |       0     |
|   Max Value   |      13      |       2          |      4     |      10     |
|    Example    |      13      |       2          |      4     |       5     |

<!-- All codes will start with 0x415A and end with 0x5942-->
Example: AZ4113245BY

All of this documentation can be found in this ["Project Code Zip File"](Dirks_subsystem.zip) for your replication and viewing leisure.
