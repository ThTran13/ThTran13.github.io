---
layout: post
title: 
description:  Chess Link is a smart physical chessboard that bridges the gap between traditional tactile play and modern online connectivity. Designed in response to the rise of remote gaming during the COVID-19 pandemic, it allows users to play chess physically while connected to friends or AI opponents via a companion Android app. The board uses 64 Hall effect sensors and RGB LEDs to track piece movements and guide gameplay with intuitive lighting. An Arduino Giga manages local hardware, while Cloudflare Workers and Durable Objects handle real-time game logic and matchmaking. With Bluetooth and WiFi connectivity, Chess Link delivers a seamless, screen-free chess experience.

skills:
    - Arduino Giga R1
    - Hall effect sensor integration
    - LED control and multiplexing
    - LCD screen interfacing
    - Breadboarding & circuit debugging
    - Soldering and wiring
    - C++ (microcontroller programming)
    - Flutter (mobile app development)
    - Dart
    - Python (logic, backend testing)
    - Bluetooth Low Energy (BLE)
    - WiFi module configuration
    - WebSocket communication
    - RESTful API consumption
    - Cloudflare Workers (serverless functions)
    - Cloudflare Durable Objects
    - SQL database management
    - Secure authentication & token systems
    - HTTPS/WSS protocols
    - KiCAD (schematic and PCB layout)
    - Circuit testing and troubleshooting

main-image: /logIn.jpg
---

---
# Header 1 
Used for the title (already generated automatically at the top)
## Header 2  
Use this for the header of each section
### Header 3 
Use this to have subsection if needed


## Embedding images 
### External images
{% include image-gallery.html images="logIn.jpg, inGame,jpg, Menu.jpg, startScreen.jpg" height="400"%}
<span style="font-size: 10px">"Starship Test Flight Mission" from https://www.flickr.com/photos/spacex/52821641477/</span>  
You can put in multiple entries. All images will be at a fixed height in the same row. With smaller window, they will switch to columns.  

### Embeed images
{% include image-gallery.html images="project2.jpg" height="400" %} 
place the images in project folder/images then update the file path.   


## Embedding youtube video
The second video has the autoplay on. copy and paste the 11-digit id found in the url link. <br>
*Example* : https://www.youtube.com/watch?v={**MhVw-MHGv4s**}&ab_channel=engineerguy
{% include youtube-video.html id="MhVw-MHGv4s" autoplay= "false"%}
{% include youtube-video.html id="XGC31lmdS6s" autoplay = "true" %}

you can also set up custom size by specifying the width (the aspect ratio has been set to 16/9). The default size is 560 pixels x 315 pixels.  

The width of the video below. Regardless of initial width, all the videos is responsive and will fit within the smaller screen.
{% include youtube-video.html id="tGCdLEQzde0" autoplay = "false" width= "900px" %}  

<br>

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


