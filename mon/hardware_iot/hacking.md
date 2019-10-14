## Link

https://allthingsopen.org/talk/hardware-hacking-101-rogue-keyboards-and-spy-cables/

## Notes

- abusing security assumptions about USB
- access just by plugging in the device
  - sometimes don't even need to be plugged in!
- HID class: human interaction
  - Keyword
  - Mice
  - Controllers
  - even USB batteries
- Inherent trust keyboards
  - No drivers needed
- USB accepts any device as long as it has a driver

### Attacks

- exfiltrating passwords and credentials
- get wifi passwords in clear (without any passwords!)
- reverse shell
  - just 3 seconds!
  - can phone home to unknown servers

Usually targets Windows.
Just need to plug into the laptop.

Usually demos https://people.redhat.com/flucifre/hacks/setec_astronomy.gif

### Intro to Ducky language

- Need to delay until operating system responds to gui commands
- Very minimal language
- Can run later when people are not paying attention
- Featured in Mr. Robot

### Clones

- Freeloaders are a sign of success
  - https://github.com/insecurityofthings/uDuck
  - https://hackernoon.com/low-cost-usb-rubber-ducky-pen-test-tool-for-3-using-digispark-and-duck2spark-5d59afc1910
  - https://hackerwarehouse.com/product/usb-ninja-cable/ - looks like USB cable

### Solutions

- Syncstop: http://syncstop.com/ (formerly "The USB Condom")
  - only allows power
  - CIO: don't worry, no one will use it
- USBSafe: https://www.crowdsupply.com/karoly-simon/usbsafe2
  - controlled in software

### Other ideas

- USB Hubs
- PISO: USB built on Pi Zero
  - Tiny screen
- Bash Bunny: https://wiki.bashbunny.com/#!index.md
  - 'Like shooting fish in a barrel'
  - shows up a storage
  - can turn into wireless/keyboard at will
  - many exploits already written
  - 1.6 Ghz
- Cactus WHID: https://github.com/whid-injector/WHID
- GSM Monitoring: A phone that happens to look like a charging cable
  - $10 on ebay
  - Doctorow called 'trickle-down surveillance'
  - You can call the cable!
  - Can geo-locate the cable

### Summary

- Hacking has a low barrier to entry
- Physical access makes it easy
- Wifi makes it easy
- Lost USB attack
  - In military, random USBs get thrown away/destroyed
  - In corporate, people plug it right in
- Cheap attacks make attacks more common
- Anywhere that needs physical security should pour glue in their USB ports
- The only reason we don't worry about it is it's so easy to attack WiFi

## References

- https://tomu.im/, about the size of a Ubikey, $2 in parts
  - 8 kB RAM
  - 64 kB Flash
  - USB 2.0
  - 25 MHz ARM
  - fits entirely in USB port without being seen

- https://shop.hak5.org/products/usb-rubber-ducky-deluxe
  - if it quacks like a keyboard, it must be a keyboard
  - to load files, need a different hardware interface (microSD card)
  - 32 kB RAM
  - 256 kB flash
  - MicroSD slot
  - USB 2.0
  - 60 MHz AVR
  - JTAG interface

- https://ducktoolkit.com/encode
- https://github.com/gentilkiwi/mimikatz

## Meta

- switched laptops _midtalk_
- targeting Windows 95+ lol
- really funny guy
