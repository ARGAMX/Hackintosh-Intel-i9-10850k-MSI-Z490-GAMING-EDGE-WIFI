# Hackintosh-Intel-i9-10850k-MSI-Z490-GAMING-EDGE-WIFI

![About this mac](Images/01.Catalina-10.15.7.png)

Hello folks,

I have successfully installed (updated) MacOS Catalina to 10.15.5 on my i9-10850k Comet Lake running on a MSI Z490 GAMING EDGE WIFI.

You can find my EFI folder in this repository.

I think my config should perfectly work with the configuration based on:

- **LGA1200**
- **Comet Lake i7/i9 10xxx**
- **Z490 Chipset**
- **MSI GAMING**

**Current Bootloader: OpenCore 0.6.6**

OpenCore setup was made according to
https://dortania.github.io/OpenCore-Install-Guide/

**Go through that guide to get basic understanding.**

# Hardware
- CPU: **Intel i9-10850k Comet Lake**
- iGPU: **Intel UHD 630**
- dGPU: **None**
- Motherboard: **MSI Z490 GAMING EDGE WIFI**:
	- Audio: Realtek ALC1200-VD1
	- Ethernet: 2.5Gbit Realtek RTL8125B-CG
	- Intel Wi-Fi 6 AX201 (a/b/g/n/ac/ax)
	- Bluetooth 5.1
	- USB-C/Thunderbolt port
- RAM: 2x Kingston DDR4 16Gb 3200MHz pc-25600 (KVR32N22S8/16)
- 1x DisplayPort 4k Monitor
- 1x HDMI FullHD Monitor

# Working
- [x] **Boot successfully** in macOS Catalina 10.15.5 and 10.15.7
- [x] **USB**
- [x] **PS/2 Keyboard**
- [x] **1x DisplayPort** for Output with 4k Monitor
- [x] **1x HDMI** for Output with FullHD Monitor
- [x] **Audio output**: ALC1200-VD1 (AppleALC.kext, layout-id=11)
- [x] **Audio input**: via USB WebCamera
- [x] **1Gbit Ethernet** (Realtek RTL8125B-CG)
- [x] **Wifi** (via internal Intel Wi-Fi 6 AX201). 
- [x] **OpenGL, OpenCL, Metal**
- [x] **iOS Simulator**
- [x] **Shutdown**
- [x] **Restart**
- [x] **Hibernate/Sleep/Wake**

# Not working so far
- **Audio input**: via Microphone (regular mini-jack 3.5 mm) (but Audio input via USB WebCamera working fine)

# Problems solved
- [x] **Stuck on 'This version of Mac OS X is not supported'**: added flag ```-no_compat_check``` to ```boot-args```
- [x] **PS/2 Keyboard not working**: installed ```VoodooPS2Controller.kext``` https://github.com/acidanthera/VoodooPS2
- [x] **Ethernet not working**: installed ```LucyRTL8125Ethernet.kext``` https://www.insanelymac.com/forum/topic/343542-lucyrtl8125ethernetkext-for-realtek-rtl8125
- [x] **WiFi not working**: installed ```itlwm.kext```: https://openintelwireless.github.io/General/Installation.html and ```HeliPort```: https://openintelwireless.github.io/HeliPort
- [x] **Audio not working**: installed ```AppleALC.kext``` and ```alcid``` (```layout-id```) set to ```11```
- [x] **4k not available**: set ```framebuffer-stolenmem``` to ```00000002``` (was ```00003001```)

- [x] **OpenCL not working**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)
- [x] **OpenGL_GpuTest_OSX_x64_0.7.0 not working**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)
- [x] **VLC not working - crashing**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)
- [x] **iOS Simulator not working**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)
- [x] **Firefox crashing on opening**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)
- [x] **Safari can't open www.fb.com**: set ```device-id``` to ```9B3E0000``` (was ```C59B0000```)

- [x] **HDMI monitor not working**: 

set 

(DisplayPort)

```framebuffer-con0-enable``` to ```01000000```

```framebuffer-con0-alldata``` to ```03040800 00040000 C7030000```

(HDMI)

```framebuffer-con1-enable``` to ```01000000```

```framebuffer-con1-alldata``` to ```01010900 00080000 C7030000```

(?)

```framebuffer-con2-enable``` to ```01000000```

```framebuffer-con2-alldata``` to ```02020A00 00080000 C7030000```
