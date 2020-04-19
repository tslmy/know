# What to do with a Raspberry Pi?

**Background:** I gave my Raspberry Pi 2 to a neighbor's kid in summer 2019. Being self-isolated at home in spring 2020 due to COVID-19, I got bored and ordered a Raspberry Pi 4 online.

_Sidenote_: I learned that I can take advantage of my employee benefits and have a 15% off, and that the item is shipped from the UK. Interesting.

## Software-wise

I took the process of setting up my Raspberry Pi 4 as an opportunity to **learn Ansible**. I will share my Ansible Playbook once I deem it has become useful to more general audiences.

Services currently enabled in my Raspberry Pi:

* Services that are actively in use:
  * **Samba**: Used as Time Machine backup destination.
  * **HomeBridge**: Connects Siri with my smartbulb.
* Services that are ready to use:
  * **Shairport Sync**: AirPlay audio destination.
  * \*\*\*\*[**JupyterHub**](https://github.com/jupyterhub/jupyterhub/wiki/Run-jupyterhub-as-a-system-service): For occasional experiments.
* Stuff I tried out, but not as useful as on a x86-compatible machine:
  * **Docker**: There's still too few images built for armv7 support. Some images I tested and are usable:
    * **OwnCloud/NextCloud**
    * **Ghost**
  * **n8n.io**: Although the Docker image for n8n.io does not have armv7 support, you can still easily install this via good old `npm`.
  * **Home Assistant**: Everything I do currently is merely controlling a smartbulb, and HomeBridge suffices for this purpose, so I felt no need to migrate over.

I used to enjoy connecting to my Raspberry Pi via VNC. Recently, however, a GUI started to mean less to me than it did a couple of years ago. Nowadays, I only spin up a VNC server on the Pi manually when I feel like to.

## Hardware-wise

During my Raspberry Pi 2 era, I had one of those [3.5-inch TFT-panel touchscreens](https://www.robotshop.com/en/35i-tft-lcd-320x480-touch-display-raspberry-pi.html?gclid=CjwKCAjw7e_0BRB7EiwAlH-goMqJn74rhHmOVL0xVeDvgts3ULsNB9bBA3n7eJHUwuaa_jjwCV5_zRoCPaYQAvD_BwE) that come with a transparent case. It was not until I had started assembling did I realize that those units need a custom OS image. The customized image was based on an outdated version of Raspbian. Lacking experience with Linux drivers, I was unable to "extract" the driver and install it to a fresh install of the OS. Therefore I considered it too much a hassle and didn't bother using the touchscreen at all.

I was also eyeing on a robotic arm or building a self-driving car. After browsing through some sub-$300 options, I deemed it too pricey a hobby to take on for so little practical use.

