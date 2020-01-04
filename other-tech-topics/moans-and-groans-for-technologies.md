# Moans and Groans for Technologies

## Moans and Groans \#1: Continuity

I would like to have a coherent, unified solution that makes switching devices during one session easy and natural.

### Motivation

**Scenario description:** You need to work on a task, like drafting an email. You pull out your smartphone and started typing/dictating, with an implicit expectation that the email can be drafted within 2 minutes. As you write, you felt the necessity to add another 1,000 words, so you wish you could continue with the task on a full-size keyboard and a nicely big monitor. What are your options?

**Why confine computation within a particular piece of hardware?** It would be great if we can carry on what we are doing on one device to another without minimal interruption.

### Existing technologies that I'm aware of

Is there already technologies to solve this problem?

* **Samsung DeX mode:** You would probably not carry a keyboard, a mouse, and a monitor every time you feel like working at your local coffee shop. If you do find a permanent spot to settle down those peripherals -- most likely your cubicle and/or your own room -- you would probably desire a device with mroe computational power.
* **Cloud Computing**: Does not solve the problem of browser loading \(In fact, the cloud applications load so slowly that [people are arguing that](https://news.ycombinator.com/item?id=15643663) cloud computing has brought our end-user experience back to last decade\)
* [**Continuity features from Apple**](https://support.apple.com/en-us/HT204681)**, especially Handoff:** requires compatiability on the applications on both the macOS version and the iOS version. 
* There was a company from the last century whose employees carried a smart card, not laptops, from/to meeting rooms. Terminals were available at their desks and in each meeting room, so one could plug in the card and get back to their desktop environment. This is great for demonstrations and team collborations. Sadly, I could not find the original article I've read about this from.

### Present Status

Currently, I'm using a extra-portable ultrabook \(MacBook, 2015\) as my daily driver, plugging it into an adapter when I need a full-form desktop experience at home. The adapter connects my MacBook to a monitor, a full-size keyboard, a mouse, and a USB-A hub with one single cable. This is by far the most versatile form-switching experience I had, but it also comes with insufficiencies:

* MacBook has no touchscreen. I draw stuff and jot down notes quite often using my iPad. I wish they were one device.
* Handing off tasks between my iDevices and my laptop relies too heavily on cloud syncing. Apps that have very different iOS and macOS editions complicate the situation further.

### Requirements

Here's what I'd like to see in a solution:

* **Ability to continue work on different forms of devices.** Full-fledged 108-key keyboard + 35 inch monitor? Laptop that weights under 2 lbs? Smartphone in your pockets? Yes please!
* **Ability to work on the same object**, not relying on transferring/syncing documents back and forth. This might imply "streaming": We can
  * stream video using technologies such as VNC \(which is slow & laggy but more compatiable; I'm actually using VNC quite frequently\),
  * stream UI components such as windows using X-server \(which is less laggy, but more difficult to implement to different platforms\), or
  * stream text only using `ssh` + `tmux`, etc. I would really love to have GUI, though.
* Little sacrifice on performance.
* Little sacrifice on computational power.

### Possible Solutions

Here are a few possible solutions we can get started now:

* **Switch to Samsung**, I guess? At present, I believe this is the best way to solve the continuity problem between phone and desktop. I believe there's a good client app for remote desktop on Android, which could be used to connect us to a more powerful, immobile, device for computation-hungry tasks.
* Switch to Linux and start **forwarding all windows** through X?

