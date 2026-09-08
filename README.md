# TCL DEBLOATER & PRIVACY HARDENING SCRIPT
**_NOTE: This script is only for TCL Android TVs._**

This script is intended to optimize TCL Android TVs by removing unnecessary applications that consume system resources and slow down the TV, while providing system hardening and recovery options.

This script is based on the work from [mickaelmendes50/optimize_android_tv](https://github.com/mickaelmendes50/optimize_android_tv).

## Prerequisites

1. **Enable Developer Options on your TCL TV:**
   - Go to **Settings > System > About** (or Device Preferences > About).
   - Scroll down to **Build** and press the **OK** button on your remote 7 times until it says "You are now a developer."
2. **Enable USB Debugging:**
   - Go back to **Settings > System > Developer options**.
   - Turn on **USB Debugging** (and Network Debugging if connecting over Wi-Fi).
3. **Install ADB on your computer:** Make sure Android Debug Bridge (`adb`) is installed and available in your terminal path.

> **Alternative:** (New users) you may also find issues so manually pasting the `updated.sh` contents into your terminal after connecting to your TV via ADB is also available and will alleviate common errors if applicable.

4. Run `adb connect 192.168.***.***` (changing to your ip address) in your terminal and then allow the connection on your TV, and paste the `updated.sh` script in your terminal.
 
---
## How to Run the Script



Choose one of the following methods to download and run the script depending on your preference.



### Method 1: Download and Run Locally (Recommended)

This is the safest method because it allows the script to properly capture interactive menu prompts without segmentation faults.



```bash

curl -fsSL https://raw.githubusercontent.com/JudahEstrada/tcl-debloat/main/updated.sh -o debloat.sh
bash debloat.sh
