# 🔓📱 Android-PIN-Bruteforce

Unlock an Android phone (or device) by bruteforcing the lockscreen PIN.

Turn your Kali Nethunter phone into a bruteforce PIN cracker for Android devices! 

## 📱 How it works

It uses a USB OTG cable to connect the locked phone to the Nethunter device. It emulates a keyboard, automatically tries PINs, and waits after trying too many wrong guesses.

![How to Connect Phones](https://user-images.githubusercontent.com/101783/91640968-b7d46280-ea64-11ea-8340-94e3bacb706e.png)

[Nethunter phone] <--> [USB cable] <--> [USB OTG adaptor] <--> [Locked Android phone]

The USB HID Gadget driver provides emulation of USB Human Interface Devices (HID). This enables an Android Nethunter device to emulate keyboard input to the locked phone. It's just like plugging a keyboard into the locked phone and pressing keys.

⏄1�7 This takes a bit over 16.6 hours to try all possible 4 digit PINs, but with the optimised PIN list it should take you much less time.

### 📱 ⛄1�7 📲 You will need

- A locked Android phone
- A Nethunter phone (or any rooted Android with HID kernel support)
- USB OTG (On The Go) cable/adapter (USB male Micro-B to female USB A), and a standard charging cable (USB male Micro-B to male A).
- That's all!

## 🌟 Benefits

- Turn your NetHunter phone into an Android PIN cracking machine
- Unlike other methods, you do not need ADB or USB debugging enabled on the locked phone
- You don't need to buy special hardware, e.g. Rubber Ducky, Teensy, Cellebrite, XPIN Clip, etc.
- You can easily modify the backoff time to crack other types of devices
- It works!

## ⭄1�7 Features

- Optimised PIN list
- Bypasses phone pop-ups including the Low Power warning
- Detects when the phone is unplugged or powered off, and waits while retrying every 5 seconds
- Configurable delays of N seconds after every X PIN attempts
- Log file

## Installation

TBC


## Usage

```

Android-PIN-Bruteforce is used to unlock an Android phone (or device) by bruteforcing the lockscreen PIN.

  Find more information at: https://github.com/urbanadventurer/Android-PIN-Bruteforce

Commands:
  crack             Begin cracking PINs
  resume            Resume from a chosen PIN
  rewind            Crack PINs in reverse from a chosen PIN
  diag              Display diagnostic information

Options:
  -f, --from PIN    Resume from this PIN
  -m, --mask REGEX  Use a mask for known digits in the PIN
  -t, --type TYPE   Select PIN or PATTERN cracking
  -l, --length NUM  Crack PINs of NUM length
  -d, --dry-run     Dry run for testing. Doesn't send any keys.
  -v, --verbose     Output verbose logs.

Usage:
  android-pin-bruteforce <command> [options]
```


## Supported Android Phones/Devices

It has been tested with these devices:
- Samsung S5 with Android 6.0.1


## 🎳 PIN Lists

### Optimised PIN list

`pinlist.txt` is an optimised list of all possible 4 digit PINs, sorted by order of likelihood.
pinlist.txt is from https://github.com/mandatoryprogrammer/droidbrute

This list is used with permission from Justin Engler & Paul Vines from Senior Security Engineer, iSEC Partners,
and was used in their Defcon talk, [Electromechanical PIN Cracking with Robotic Reconfigurable Button Basher (and C3BO)](https://www.defcon.org/html/defcon-21/dc-21-speakers.html#Engler)

### Cracking with Masks

Masks use regular expressions with the standard grep extended format.

`./android-pin-bruteforce crack --mask "...[45]" --dry-run`

- To try all years from 1900 to 1999, use a mask of `19..`
- To try PINs that have a 1 in the first digit, and a 1 in the last digit, use a mask of `1..1`
- To try PINs that end in 4 or 5, use `...[45]`


## 🚀 Roadmap

- [DONE] Works
- [DONE] Detects USB HID failures
- [DONE] Improve Usage and commandline options/config files
- [DONE] Add bruteforce for n digit PINs
- [DONE] Mask for known digits
- [DONE] Crack PIN list in reverse (to find which recent PIN unlocked the device)
- Add progress bar
- Add ETA
- ASCII art
- Nicer GUI for NetHunter
- Find/test more devices to bruteforce (iPhone)
- Try to detect when phone is unlocked (Use Nethunter camera as a sensor?)
- Crack Android Patterns (try common patterns first)


## 🔧 Troubleshooting

### Executing the script

If you installed the script to /sdcard/, you can execute it with the following command.

```bash ./android-pin-bruteforce``` 

Note that Android mounts /sdcard with the noexec flag. You can verify this with ```mount```.

### Check the cables

The OTG cable should be connected to the locked Android phone. The regular USB cable should be connected to the Nethunter phone.

### Diagnostics

Use the diagnostic command.

```bash ./android-pin-bruteforce diag```

Note that Nethunter USB HID support was inconsistent during testing and development. However after it starts working, it should continue working until you crack the PIN.

If you receive this message when the USB cable is plugged in then try taking the battery out of the locked Android phone and power cycling it.

```[FAIL] HID USB device not ready. Return code from /system/xbin/hid-keyboard was 5.```

### Tips

- Try powering off the phone and taking out the battery
- Try sending keys to your PC or laptop
- Note that the ```Device not Found``` messages are not as important as sending keys successfully.


## 💣 Known Issues

- This cannot detect when it unlocks

## 🛰 Technical Details

This works from an Android phone because the USB ports are not bidirectional, unlike the ports on a laptop.

Keys are sent using `/system/xbin/hid-keyboard`.
To test this and send the key 1 you can use `echo 1 | /system/xbin/hid-keyboard dev/hidg0 keyboard`

Before each PIN, we send the escape and enter keys. This is to keep the Android responsive and dismiss any popups about the number of incorrect PIN attempts or a low battery warning.


## 🙋 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## 😎 Authors and acknowledgment

Developed by Utsanjan Maity (Dope Satan).

### Motivation

My original motivation to develop this was to unlock a Samsung S5 Android phone. It had belonged to someone who had passed away, and their family needed access to the data on it. As I didn't have a USB Rubber Ducky or any other hardware handy, I tried using a variety of methods, and eventually realised I had to develop something new.

### Credit

The optimised PIN list is from Justin Engler (@justinengler) & Paul Vines from Senior Security Engineer, iSEC Partners
and was used in their Defcon talk, [Electromechanical PIN Cracking with Robotic Reconfigurable Button Basher (and C3BO).](https://www.defcon.org/html/defcon-21/dc-21-speakers.html#Engler).

### Graphics

Designed by Utsanjan Maity and gratefully using these free vector packs:

- [USB Ports Isometric Free Vector by VisionHeldup](https://www.vecteezy.com/vector-art/159576-usb-ports-isometric-free-vector)
- [HDMI and USB Vector Set by Mary Winkler](https://www.vecteezy.com/vector-art/107006-hdmi-and-usb-vector-set)
- [Isometric Data Security Illustration by Rizal.Medanguide](https://www.vecteezy.com/vector-art/661831-isometric-data-security-illustration)
- Kali NetHunter Logo

## 🗿 Comparison with other projects and methods to unlock a locked Android phone

### What makes this project unique? 

I've been asked what makes this project unique when there are other open-source Android PIN cracking projects.

Android-PIN-Bruteforce is unique because it cracks the PIN on Android phones from a NetHunter phone and it doesn't need the locked phone to be pre-hacked.

It works:
- Without having to buy special hardware, such as a Rubber Ducky, Celebrite, or XKEY.
- Without ADB or root access (the phone doesn't have to be pre-hacked).

| Project                                               | ADB/USB Debugging  | Requires root | Requires $ hardware | Commercial  |
------------------------------------------------------- | ------------------ | ------------- | ------------------- | ----------- | 
| ⭄1�7 Android-PIN-Bruteforce                             | No                 | No            | Nethunter phone     | No          | 
| github.com/PentesterES/AndroidPINCrack                | Yes                | Yes           | No                  | No          |
| github.com/ByteRockstar1996/Cracking-Android-Pin-Lock | Yes                | Yes           | No                  | No          |
| github.com/sch3m4/androidpatternlock                  | Yes                | Yes           | No                  | No          |
| github.com/georgenicolaou/androidlockcracker          | Yes                | Yes           | No                  | No          |
| github.com/MGF15/P-Decode                             | Yes                | Yes           | No                  | No          |
| github.com/BitesFor/ABL                               | Yes                | Yes           | No                  | No          |
| github.com/wuseman/WBRUTER                            | Yes                | No            | No                  | No          |
| github.com/Gh005t/Android-BruteForce                  | Yes                | No            | No                  | No          |
| github.com/mandatoryprogrammer/droidbrute             | No                 | No            | Rubber Ducky $      | No          |
| github.com/hak5darren/USB-Rubber-Ducky                | No                 | No            | Rubber Ducky $      | Yes         |
| github.com/bbrother/stm32f4androidbruteforce          | No                 | No            | STM32F4 dev board $ | No          |
| hdb-team.com/product/hdbox/                           | No                 | No            | HDBOX  $$           | Yes         |
| xpinclip.com                                          | No                 | No            | XPINClip  $$        | Yes         |
| cellebrite.com/en/ufed/                               | No                 | No            | Cellebrite UFED $$$ | Yes         |

Some of these projects/products are really awesome but they achieve a different goal to Android-PIN-Bruteforce.

If a project requires a gestures.key or password.key, I've listed it as requiring root.
If a project requires a custom bootloader, I've listed that as requiring both ADB and root.
If you would like your project listed in this table then please open a new issue.
There are links to each of these projects in the 📚 Related Projects & Futher Reading section.

### 😭 Regular phone users

- Try the top 20 PINs from the [DataGenetics PIN analysis](https://datagenetics.com/blog/september32012/index.html) that apparently unlocks 26.83% of phones.
- Use an SMS lock-screen bypass app (requires app install before phone is locked)
- Use Samsung Find My Mobile (requires you set it up before phone is locked)
- Crash the Lock Screen UI (Android 5.0 and 5.1)
- Use the Google Forgot pattern, Forgot PIN, or Forgot password (Android 4.4 KitKat and earlier)
- Factory Reset (you lose all your data)

### 🤖 Users who have already replaced their Android ROM

If the phone already has been rooted, has USB debugging enabled, or has adb enabled.

- Flash the `Pattern Password Disable` ZIP using a custom recovery (Requires TWRP, CMW, Xrec, etc.)
- Delete `/data/system/gesture.key` or `password.key` (requires root and adb on locked device)
- Crack `/data/system/gesture.key` and `password.key` (requires root and adb on locked device)
- Update sqlite3 database `settings.db` (requires root and adb on locked device)

### 🔬 Forensic Investigators

These methods can be expensive and are usually only used by specialised phone forensic investigators.

Note that the Cellebrite and XPIN Clip can also use the USB HID Keyboard Bruteforce method.

- Physical Extraction using Cellebrite UFED
- XPIN Clip
- Oxygen Forensic Suite (Requires USB debugging enabled)
- JTAG extraction
- Chip Off

### 🕵 Security Professionals and Technical Phone Users

Use the USB HID Keyboard Bruteforce with some dedicated hardware.

- A RubberDucky and Darren Kitchen's Hak5 brute-force script
- Write a script for a USB Teensy
- Buy expensive forensic hardware
- Or you can use this with your NetHunter phone!

Attempts to use an otherwise awesome project Duck Hunter, to emulate a RubberDucky payload for Android PIN cracking did not work. It crashed the phone probably because of the payload length.


## 📚 Related Projects & Futher Reading

### USB HID Hardware without NetHunter

hak5 12x17: Hack Any 4-digit Android PIN in 16 hours with a USB Rubber Ducky 
https://archive.org/details/hak5_12x17

Hak5: USB Rubber Ducky
https://shop.hak5.org/products/usb-rubber-ducky-deluxe

USB-Rubber-Ducky Payloads
https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads

Teensy
https://www.pjrc.com/teensy/

Brute Forcing An Android Phone with a STM32F4Discovery Development Board
https://github.com/bbrother/stm32f4androidbruteforce
https://hackaday.com/2013/11/10/brute-forcing-an-android-phone/

Automated brute force attack against the Mac EFI PIN (Using a Teensy)
https://orvtech.com/atacar-efi-pin-macbook-pro-en.html
https://hackaday.io/project/2196-efi-bruteforcer

Droidbrute: An Android PIN cracking USB rubber ducky payload made efficient with a statistically generated wordlist.
https://github.com/mandatoryprogrammer/droidbrute

Discussion forum about the hak5 episode, and Android Brute Force 4-digit pin
https://forums.hak5.org/topic/28165-payload-android-brute-force-4-digit-pin/

### NetHunter HID keyboard attacks

NetHunter HID Keyboard Attacks
https://www.kali.org/docs/nethunter/nethunter-hid-attacks/

### Linux Kernel HID support

Human Interface Devices (HID)
https://www.kernel.org/doc/html/latest/hid/index.html#

Linux USB HID gadget driver
https://www.kernel.org/doc/html/latest/usb/gadget_hid.html

### Cracking Android PIN and Pattern files

AndroidPINCrack - bruteforce the Android Passcode given the hash and salt (requires root on the phone)
https://github.com/PentesterES/AndroidPINCrack

Android Pattern Lock Cracker - bruteforce the Android Pattern given an SHA1 hash (requires root on the phone)
https://github.com/sch3m4/androidpatternlock

### General Recovery Methods

[Android][Guide]Hacking And Bypassing Android Password/Pattern/Face/PI
https://forum.xda-developers.com/showthread.php?t=2620456

Android BruteForce using ADB & Shell Scripting
https://github.com/Gh005t/Android-BruteForce

### Forensic Methods and Hardware

PATCtech Digital Forensics: Getting Past the Android Passcode
http://patc.com/online/a/Portals/965/Android%20Passcode.pdf

XPIN Clip
https://xpinclip.com/

HDBox from HDB Team
https://hdb-team.com/product/hdbox/

Cellebrite UFED
https://www.cellebrite.com/en/ufed/

### PIN Analysis

Electromechanical PIN Cracking with Robotic Reconfigurable Button Basher (and C3BO)
https://www.defcon.org/html/defcon-21/dc-21-speakers.html#Engler

DataGenetics PIN analysis https://datagenetics.com/blog/september32012/index.html


