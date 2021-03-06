# Home assistant package to manage IR AC and lovelace cards configurations
I have started it as a day-to-day improvement, but it ended with 400 lines of code. Hope it will be used by someone. 

**Basic task:**
- To create a lovely page to controll all temperature and humidiy data for Lovelace from Home Assistant

**Hardware and software:**
  
  **Software:**
  - Home assistant (0.114.3 at this moment)
  - HACS
    - https://github.com/bramkragten/swipe-card
    - https://github.com/kalkih/mini-graph-card
    - https://github.com/custom-cards/button-card
    - https://github.com/thomasloven/lovelace-card-mod
    - https://github.com/custom-cards/stack-in-card
    - https://github.com/nervetattoo/simple-thermostat
    
  **Hardware:**
  - Broadlink RM Pro/Mini - Will send the commands to the AC
  - Cooper&Hunter CH-S09XN7 (or any AC with IR remote)
  - PZEM 004v3 + Sonoff Basic (or any esp32/8266 board with Tasmota) - Used to monitor if the AC is ON or OFF and power consumption as a benefit

**As a result:**
- Package to manage AC: 
  - [Package](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/ir_ac_management.yaml)
  - [Button card template](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/ui-lovelace.yaml)
  - [Frontend Custom Card](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/custom_climate_card.yaml)
  
[General design for Temperature Lovelace View (one card, multiply it for your rooms/zones)](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/custom_climate_page_card.yaml)

#####################################################

![all](media/ac_gif.gif)
![Preview](media/ac_desktop1.jpg)
![Preview](media/ac_desktop2.jpg)

**Logic:** 
General [UI layout](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/custom_climate_page_card.yaml)
- Each room/space has its own place/card. Inside it there are swiped cards:
  - First card - Picture with sensors data
  - Second - mini-graph. Humidity is a key metric to monitor as it's really important to stay helthy at home. 
  - Third+ cards - some card to mamage the climate.
  - Swipe jumps back to the enitial view in 10 seconds

AC IR management [package](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/ir_ac_management.yaml):
- Main data is collected from virtual climate device to mega-sensor. 
- Data from sensor is concatinated to script name
- You need to create a matrix of scripts for each command. In my case 4*2*2 24/25/26/27 C * Swing Up/Down * Cool/Heat
- Scripts have own name convention, like: k1_ac_cool_24_up 
- Some automation to manage it
- I'm using PZEM 004 to monitor energy and ON and OFF status, but you can use any small door sensor, or anything else. 
- I made a [combination of cards](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/custom_climate_card.yaml) to make it work and look as I think is good. + [Some button card templates](https://github.com/akarpenkoua/HA_IR_climate_control/blob/master/ui-lovelace.yaml) to save code space

Please take a look at the code comment at the package. 
Have fun and Enjoy.

