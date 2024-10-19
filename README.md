<div align="center">

<img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/azor_flashing_logo.png" alt="azor_banner" width="550"/>

<hr style="border: none; height: 2px; background-color: purple; width: 100%;">

![Static Badge](https://img.shields.io/badge/MSI-AZOR-purple)
![Static Badge](https://img.shields.io/badge/Flashing-Station-red)
![Static Badge](https://img.shields.io/badge/Marquardt-U.S.-lightblue)
![Static Badge](https://img.shields.io/badge/Author-Ethan_Baker-green)
![Static Badge](https://img.shields.io/badge/August-2024-orange)

</div>

# ⚡ AZOR Flashing

AZOR Flashing is a Python-native solution to a faulty printed-circuit board flashing station on the AZOR assembly line at Marquardt U.S.. This station is responsible for more than $10,000,000 in product and provides the functionality to flash, download, and run application code, pair key fob and gateway boards with unique hex values, and crystal trim board headers to optimize Bluetooth frequency strength. 

Using Python multithreading and hardware optimization for quick JTAG connections, this rebuild reflects a significant improvement in efficiency over the previous station, cutting down production time by 89% while utilizing a less resource-intensive setup. 

A responsive and functional GUI accompanies the Python automation, providing clear status indicators and live instructions to allow for efficient use by untrained operators. This, alongside detailed process checks, ensures a favorable fallout rate of less than 1%.

# 🎥 Videos
# <a href="https://youtu.be/2AJPzRWuK8c" target="_blank">Usage Demo</a>
<div align="left">
  <a href="https://youtu.be/2AJPzRWuK8c" target="_blank">
    <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/thumbnail.png" alt="thumbnail" width="350"/>
  </a>
  <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
</div>


# ✨ Functionality

## User Interface

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/gui.PNG" alt="gui" width="550"/>
    <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
  </div>


A clear, simple, and informative UI was necessary for untrained operators to use effectively. The left sidebar records Machine Information, including shift and lifetime totals for the amount produced, amount failed, current cycle time, and average cycle time, while the right sidebar contains ANDON-inspired status icons for the different stages of the flashing process. 

The bottom of the screen contains two terminal-like text boxes, which display outputs from SmartSnippets and winIDEA, the programs used to flash the PCBs, in real-time. This allows for Engineers to quickly troubleshoot when boards are not flashed correctly, and give operators the chance to see the program to ensure it is working.

Finally, the center of the screen displays instructions and current program status, allowing operators to easily follow instructions to switch out and stage components in the correct order. This location is also used to notify operators when a board fails flashing and allows them to restart the program when necessary.

## Flashing

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/flash.PNG" alt="flashing" width="550"/>
    <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
  </div>

The program utilizes SmartSnippets Toolbox CLI and winIDEA API to flash code to the PCBs. It uses a set of custom-made nests that allow for a fast JTAG connection, providing a significant increase in efficiency over the UART connection that was previously used. 


## Crystal Trimming

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/xtal.PNG" alt="flashing" width="550"/>
    <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
  </div>

The program optimizes the low-energy Bluetooth signal strength of each PCB by modifying the OTP (One Time Programmable) header of each board to set the Calibration Flag and Crystal Trim values. To do so, the existing nests were modified to introduce a power supply directly to the board itself, providing a workaround that allowed the OTP memory to be modified over the JTAG connection. 

## Process Tests

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/test.PNG" alt="flashing" width="550"/>
    <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
  </div>

Each step of the flashing program is checked by a series of efficient and conducive process tests. As the program is running, outputs from the terminals towards the bottom of the screen are scanned for success messages, while other things like the OTP header and the winIDEA application code are checked separately by reading the PCB's memory or checking the output logs. 

When the program detects a failure, execution of all of the concurrent flashing processes stops immediately, and the operator is instructed to place the part in the Reject bin and to press ENTER to try again with a new kit. 

## Multithreading

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/multithread.PNG" alt="flashing" width="550"/>
    <hr style="border: none; height: 1px; background-color: purple; width: 100%;">
  </div>

To further improve efficiency, (and ultimately cut production time by 89%), the program utilizes concurrent flashing threads that allow for the Fobs and the Gateway to be flashed at the same time. This introduced challenges relating to race conditions and similar complications, requiring multiple global flags and mutex locks to be utilized.

At the same time, the program uses other threads to display the GUI, count cycle time, and provide functionality for the stop/reset buttons. Working through this further highlighted the need for organized flags and mutex locks to allow for a consistent and reliable program execution.

# 📀 Technologies / Dependencies

![Static Badge](https://img.shields.io/badge/PYTHON-darkblue?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/LABVIEW_G-gold?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/TKINTER-blue?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/winIDEA-purple?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/SmartSnippets-green?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/HexFile_Generator.exe-orange?style=for-the-badge)

# 🔨 Hardware
- Dell Latitude 5580 w/ Windows 10

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/dell.png" alt="dell" width="200"/>
  </div>

- Fob and Gateway Nests

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/nests.png" alt="nests" width="200"/>
  </div>

- 2x Dialog DA14580 Development Boards

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/devkit.jpg" alt="devkit" width="200"/>
  </div>
  
- iSYSTEM iC5000 BlueBox

  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/BlueBox.png" alt="bluebox" width="200"/>
  </div>
  
- Triple Power Supply
  <div align="left">
  <img src="https://raw.githubusercontent.com/ethbak/azor-flashing/main/images/power.png" alt="powersupply" width="200"/>
  </div>


# 🏎️ Performance

### Average Cycle Time
- Current: `1m 02s`
- Original: `4m 33s`
  
### Fallout Rate
- Current: `<1%`
- Original: `>50%`

_These improvements reflect savings of over 4,000 labor hours and $100,000 in related costs over the project's lifetime._ 

# 🖥️ Where's the Code?
This application was developed for sole use by Marquardt U.S. and is therefore not available for open source or public use as per my employment agreement.

This README file simply serves to provide a detailed depiction of my contribution to the project during my time as a Software Engineer at Marquardt.

# 👨‍💻 Contributors

### [Ethan Baker](https://www.ebaker.us) - Software Development, Hardware Development
### Matthew Teabo - Hardware Development
