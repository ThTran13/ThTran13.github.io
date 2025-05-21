---
layout: post
title: 
description:  Chess Link is a smart physical chessboard that bridges the gap between traditional tactile play and modern online connectivity. Designed in response to the rise of remote gaming during the COVID-19 pandemic, it allows users to play chess physically while connected to friends or AI opponents via a companion Android app. The board uses 64 Hall effect sensors and RGB LEDs to track piece movements and guide gameplay with intuitive lighting. An Arduino Giga manages local hardware, while Cloudflare Workers and Durable Objects handle real-time game logic and matchmaking. With Bluetooth and WiFi connectivity, Chess Link delivers a seamless, screen-free chess experience.

skills:
    - Hall effect sensor integration
    - LED control and multiplexing
    - LCD screen interfacing
    - Breadboarding & circuit debugging
    - C++
    - Flutter 
    - Dart
    - Python
    - RESTful API consumption
    - Cloudflare Workers
    - SQL database management
    - HTTPS/WSS protocols
    - KiCAD

main-image: /logIn.jpg
---

---

## Overall Architecture
{% include image-gallery.html images="OverallArchitecture.jpeg" height="400" %}
<span style="font-size: 10px">A depiction of the overall project communication flow</span>

## Frame Design
{% include image-gallery.html images="Frame.jpeg" height="400" %}
<span style="font-size: 10px">Frame Design</span>

The mechanical part of the board consisted of the frame, the struts, the cover, and the squares. 
The board was fully constructed from birch plywood due to it being very cost-effective and sturdy. The squares themselves were 3D printed with an acrylic insert. By making them out of more common materials, it is easy to customize the board by changing different parts to better fit what the user wants.

## Circuit Design
{% include image-gallery.html images="HallSensorCircuitSchematic.jpeg, PCB.jpeg" height="400" %}
<span style="font-size: 10px">Circuit and PCB Design</span>

The sensor system of the ChessLink board was designed using a switch matrix configuration, where Hall effect sensors were arranged in an 8×8 grid to detect piece positions. The VIN pins of the sensors were routed across rows, while the output signal pins ran down columns. Each sensor’s ground was controlled by 2N2222 transistors acting as row switches, which were driven by eight digital I/O pins from the Arduino Giga. Another eight analog inputs were used to read signals from each column. By sequentially activating one row at a time and reading the outputs from the columns, the board could detect magnetic piece placement. This method required a brief delay between row switching and signal reading, resulting in a full board scan time of approximately 200 milliseconds.

To indicate moves, each square was outfitted with two LEDs mounted on parallel-connected strips. To reduce computational demand on the Arduino Giga, these LEDs were controlled by a separate Arduino Uno, which received RGB commands and position data via a serial interface. Power was supplied by a Samsung 21700 USB-C rechargeable battery, enabling portable use. Because the system included both 3.3V and higher-voltage components, two boost converters were used to step up the voltage for powering 5V LEDs and 9V Arduino boards, with an overall efficiency of approximately 90%. This integrated system enabled responsive, untethered gameplay with both visual feedback and accurate piece detection.

## Chess App
{% include image-gallery.html images="startScreen.jpg, logIn.jpg, Menu.jpg, inGame.jpg" height="400" %}
<span style="font-size: 10px">App Design</span>

The Chess Link mobile application was developed using Flutter, chosen for its cross-platform 
compatibility and ease of integrating Bluetooth and network-based communication. The Chess 
Link app provides a full-featured user interface that enhances the gameplay experience beyond 
just board connectivity.

The app uses Bluetooth Low Energy (BLE) to establish a direct connection with the smart 
chessboard. Once paired, the app sends control signals such as player moves, game initiation 
commands, and board reset instructions. It also receives updates from the board, such as 
confirmation of valid moves and illegal move alerts. The BLE communication is handled 
through Flutter plugins like flutter_blue_plus, which provides access to the Giga’s BLE services. 

It communicates with the backend mostly through a combination of WebSocket 
connections for real-time gameplay updates and HTTP API requests for actions like user 
authentication, match creation, and statistics retrieval. The app listens for move updates and 
game state changes through the WebSocket channel and reflects them both on the app’s interface 
and the physical board.

## Demo
<br>
{% include youtube-video.html id="xJGokFGASY4" autoplay="false" %}

<br>

The Arduino code can also be broken down into a few main parts of functionality. It consists of 
the LEDs, LCD display, buttons, WiFi, and BLE communication, and the Hall Effect sensors for 
move detection. In order to maintain varying requirements of these different systems, it is  
important that no system utilizes significant portions of blocking time. If the move detection 
prevented updates to the LCD, for example, then player messages or errors from the backend 
might not be handled properly. To this end, the software was engineered as a large state machine. 
Player inputs generate flags to be handled within the overall loop that the Arduino runs on. 

The first step is to receive player and game IDs via Bluetooth from the accompanying app. To 
accomplish this, a few characteristics are packaged into a Bluetooth service to be advertised. The 
phone app updates the characteristics with the relevant data, allowing the Arduino Giga R1 to 
begin its connection to WiFi and the backend. Once a stable websocket connection has been 
established, the loop consists of checking that the connections are still stable, updating the LCD 
and LEDs, handling incoming websocket messages, and detecting current voltage readings from 
each of the Hall effect sensors. To allow for readable information to appear on the LCD without 
quickly being overwritten by new incoming messages, a queue was implemented with the 
message to be displayed, the time to display it for, and after how much time it will leave the 
queue. The time-out feature is to prevent stale information from displaying on the board. For 
example, if a move has been detected but before it has been displayed on the LCD, the player has 
changed their move. In this case, the timeout will prevent the stale move data from being shown 
to the user. Similar logic was implemented on the LEDs to manage players making moves and 
displaying player-to-player messages, such as emojis. 

## Adding a hozontal line
---

## Starting a new line
leave two spaces "  " at the end or enter <br>

## Adding bold text
this is how you input **bold text**

## Adding italic text
Italicized text is the *cat's meow*.

## Adding ordered list
1. First item
2. Second item
3. Third item
4. Fourth item

## Adding unordered list
- First item
- Second item
- Third item
- Fourth item

## Adding code block
```ruby
def hello_world
  puts "Hello, World!"
end
```

```python
def start()
  print("time to start!")
```

```javascript
let x = 1;
if (x === 1) {
  let x = 2;
  console.log(x);
}
console.log(x);

```

## Adding external links
[Wikipedia](https://en.wikipedia.org)


## Adding block quote
> A blockquote would look great if you need to highlight something


## Adding table 

| Header 1 | Header 2 |
|----------|----------|
| Row 1, Col 1 | Row 1, Col 2 |
| Row 2, Col 1 | Row 2, Col 2 |

make sure to leave aline betwen the table and the header


