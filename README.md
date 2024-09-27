# Configuring a D-Link DIR-882 A1 Router with OpenWRT for PPPoE and Wireless Connectivity

## Disclaimer

This guide is provided for **experimental and learning purposes only**. The issues and solutions described here reflect my personal experience and should not be taken as an indication of any inherent flaws or problems with the vendors' devices or firmware. There is a possibility that the issues I encountered were specific to my own devices. I decided to address these problems as part of my personal interest in networking and router technologies. I do not blame any of the manufacturers involved (D-Link, Huawei, or Tenda) for any misfunctionalities. My aim is solely to document the steps I took to resolve the issues and to share the learning experience with others.

---

## Problem Overview

Initially, I encountered two major issues with my Huawei modem (provided by my ISP) and D-Link DIR-882 A1 router:

1. **Wi-Fi and PPPoE Mode Issues with Original Firmware**:  
   My Huawei modem stopped transferring Wi-Fi to my D-Link DIR-882 A1 router, which was set up as an access point via Ethernet. Additionally, the modem did not provide internet access through Wi-Fi to any device (e.g., mobile phones, laptops). When I attempted to configure PPPoE directly on the D-Link router using its original firmware, the setup was unsuccessful, and I could not enable dual-band Wi-Fi (2.4 GHz and 5 GHz). 

2. **Compatibility Issues with Tenda AC10U Repeaters**:  
   After successfully setting up OpenWRT on my D-Link router and configuring PPPoE with WPA3 security, I tried connecting two Tenda AC10U routers as wireless repeaters to extend the Wi-Fi range. However, the Tenda devices only supported WPA/WPA2-PSK (CCMP) encryption, causing incompatibility with the WPA3 configuration. 

## Steps Taken to Resolve the Issues

### 1. Contacting the ISP
To troubleshoot the Wi-Fi issues, I contacted my ISP and asked them to switch my Huawei modem from router to **bridge mode**. After they made the switch, the modem no longer handled Wi-Fi routing directly.

### 2. Resetting the D-Link DIR-882 A1 Router
Next, I reset the D-Link router to its factory settings to ensure a clean configuration process and be able to flash the OpenWRT firmware in recovery mode.

### 3. Flashing OpenWRT to the D-Link DIR-882 A1 Router

To gain more control and features, I decided to flash OpenWRT to the D-Link DIR-882 A1. The process I followed is outlined below:

- **Download OpenWRT**: I downloaded the correct firmware for the DIR-882 A1 from [OpenWRT's related website](https://openwrt.org/toh/d-link/dir-882_a1/).
- **Access Router Admin Panel**: I connected to the router’s admin interface by visiting `192.168.0.1` in the browser.
- **Upload Firmware**: I powered off the router and with the reset key I entered to the recovery mode, uploaded the OpenWRT firmware, and flashed the router.
- After flashing, the router rebooted with OpenWRT installed.

#### Websites Used for Flashing OpenWRT
- I followed the steps outlined in the ["Flash OpenWrt Firmware" section of this guide](https://vitaminac.github.io/D-LINK-DIR-882-A1-OpenWrt/).
- Additionally, I used [this page](https://openwrt.org/toh/d-link/dir-882_a1) in general to download the "Factory image" and for reference during the setup process.

### 4. Configuring PPPoE with OpenWRT

Once OpenWRT was installed, I configured the router to handle PPPoE directly:

- **Access OpenWRT Interface**: I logged into the OpenWRT web interface at `192.168.1.1`.
- **Edit WAN Interface**: Under **Network** > **Interfaces**, I selected **WAN** to edit.
- **Select PPPoE Protocol**: In the **General Settings**, I changed the protocol to **PPPoE**.
- **Enter ISP Credentials**: I entered the username and password provided by the ISP in the **PAP/CHAP username** and **password** fields.
- **Apply Changes**: I saved and applied the settings, and my internet connection was successfully established.

### 5. Configuring Dual-Band Wireless (2.4 GHz and 5 GHz)

After setting up the PPPoE connection, I configured the router's wireless settings for dual-band operation:

- Under **Network** > **Wireless**, I enabled both the **2.4 GHz** and **5 GHz** radios.
- I configured both radios to use **WPA3 security** for enhanced encryption and saved the settings.

### 6. Compatibility Issues with Tenda AC10U Repeaters

I ran into a new issue when I tried to connect two **Tenda AC10U routers** as wireless repeaters to extend my Wi-Fi network. The Tenda routers only supported **WPA/WPA2-PSK (CCMP)** encryption, which caused them to fail when connecting to my OpenWRT router configured with WPA3.

#### Solution: Changing Wi-Fi Security to WPA2

To resolve this, I downgraded the Wi-Fi security to ensure compatibility:

- I went back to the OpenWRT interface and navigated to **Network** > **Wireless**.
- For both the 2.4 GHz and 5 GHz networks, I changed the encryption settings from **WPA3** to **WPA2-PSK (CCMP)**, which is the highest security supported by the Tenda AC10U repeaters.
- After applying these changes, the Tenda routers successfully connected to the D-Link router, and the Wi-Fi range was extended.

---

## Key Points and Relevant Technologies for Recruiters

For professionals or recruiters assessing my technical competence, the following key points and technologies are relevant:

- **OpenWRT**: Experience flashing and configuring OpenWRT on a router for custom firmware control.
- **PPPoE Configuration**: Configuring routers to work with a PPPoE connection, including ISP interactions and handling login credentials.
- **Router Firmware Modding**: Hands-on experience with flashing firmware on a D-Link DIR-882 A1 router and troubleshooting issues with stock firmware.
- **Wi-Fi Security Protocols**: Familiarity with configuring different Wi-Fi security protocols (WPA3, WPA2) and understanding compatibility between devices.
- **Dual-Band Wi-Fi Configuration**: Configuring and optimizing both 2.4 GHz and 5 GHz wireless networks for better performance and coverage.
- **Network Troubleshooting**: Diagnosing and solving connectivity issues across multiple devices, including routers and wireless repeaters.
- **Wireless Repeater Configuration**: Configuring Tenda AC10U routers as wireless repeaters to extend network range.

This knowledge and experience reflect a solid foundation in network administration, device configuration, and troubleshooting.

---

## Hardware and Software Used

### 1. **D-Link DIR-882 A1 Router**

- A dual-band wireless router that supports both 2.4 GHz and 5 GHz frequencies. Originally, it came with D-Link’s stock firmware, which had limitations when configuring PPPoE and dual-band Wi-Fi. After flashing OpenWRT, the router gained more flexibility and advanced features.

### 2. **Tenda AC10U Routers**

- These are dual-band wireless routers, used as repeaters in this setup. While they can function as access points and repeaters, they only support WPA/WPA2-PSK (CCMP) security, which led to compatibility issues when trying to connect to the D-Link router using WPA3.

### 3. **Huawei Modem (ISP-Provided)**

- The modem provided by my ISP, which initially handled both internet and Wi-Fi distribution. After switching to **bridge mode**, it only handled internet distribution, leaving Wi-Fi routing to the D-Link DIR-882 A1.

### 4. **OpenWRT Firmware**

- An open-source Linux-based firmware for embedded devices, such as routers, that allows for extensive customization of router functionalities. OpenWRT offers greater control over network configurations, security, and device performance compared to stock firmware.

### 5. **WPA3 and WPA2-PSK (CCMP) Security Protocols**

- **WPA3**: The latest wireless encryption standard offering improved security. However, some older devices, like the Tenda AC10U, do not support WPA3, necessitating a switch to **WPA2-PSK (CCMP)**, which provides slightly less security but greater device compatibility.

---

## Conclusion

Flashing OpenWRT onto my D-Link DIR-882 A1 router resolved multiple issues I was facing, including problems with the original firmware’s PPPoE mode and wireless setup. Additionally, switching the Wi-Fi security from WPA3 to WPA2-PSK allowed my Tenda AC10U routers to work as repeaters, extending my network's range.

## Key Takeaways

- **OpenWRT** provides more flexibility and better performance for handling PPPoE connections and advanced Wi-Fi configurations compared to stock firmware in my case.
- When using wireless repeaters, make sure all devices support the same Wi-Fi security protocols. In my case, downgrading from WPA3 to WPA2 was necessary for compatibility with the Tenda AC10U routers.
  
## Additional Resources

- [OpenWRT Official Website](https://openwrt.org/)
- [D-Link DIR-882 A1 OpenWRT Firmware](https://openwrt.org/toh/d-link/dir-882_a1)
- [PPPoE Configuration Guide on OpenWRT](https://openwrt.org/docs/guide-user/network/wan/wan_interface_protocols/)
- [Wi-Fi Security Overview: WPA3 vs WPA2](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access)

---

I hope this guide helps others facing similar issues with their home networking setup.

![Generated AI Design](gen_ai_design.jpg)
