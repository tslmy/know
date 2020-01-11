# Moans and Groans for Technologies

## Continuity

I would like to have a coherent, unified solution that makes switching devices during one session easy and natural.

### Motivation

**Scenario description:** You need to work on a task, like drafting an email. You pull out your smartphone and started typing/dictating, with an implicit expectation that the email can be drafted within 2 minutes. As you write, you felt the necessity to add another 1,000 words, so you wish you could continue with the task on a full-size keyboard and a nicely big monitor. What are your options?

**Why confine computation within a particular piece of hardware?** It would be great if we can carry on what we are doing on one device to another without minimal interruption.

### Existing technologies that I'm aware of

Is there already technologies to solve this problem?

* **Desktop mode for docked smartphones:** You would probably not carry a keyboard, a mouse, and a monitor every time you feel like working at your local coffee shop. If you do find a permanent spot to settle down those peripherals -- most likely your cubicle and/or your own room -- you would probably desire a device with more computational power. Examples include:
  * **Samsung DeX mode:** This only works for Samsung devices, apparently.
  * \*\*\*\*[**maru**](https://maruos.com/): An Android variant that mimics Samsung DeX mode. Needs an Android phone, apparently.
  * \*\*\*\*[**Android Q adds a native desktop mode support**](https://www.androidpolice.com/2019/03/14/android-q-brings-native-desktop-mode-support/): This is also the only option I could try out with my current hardwares. To enable:

    1. On your computer, install `adb` via `brew cask install android-platform-tools`
    2. On your phone, in "Settings" &gt; "About phone", tap "Build number" 7 times to enable Developer mode.
    3. In "Settings" &gt; "System" &gt; "Developer options" &gt; enable "USB debugging" and "Force desktop mode".
    4. Connect your phone to your computer. Authorize on your phone.
    5. Run this: `adb shell am start -n "com.google.android.apps.nexuslauncher/com.android.launcher3.SecondaryDisplayLauncher"`

    Oddly, it never worked on my monitor and our TV. Maybe it's the adapter to blame?
* **Cloud Computing**: Does not solve the problem of browser loading \(In fact, the cloud applications load so slowly that [people are arguing that](https://news.ycombinator.com/item?id=15643663) cloud computing has brought our end-user experience back to last decade\)
* [**Continuity features from Apple**](https://support.apple.com/en-us/HT204681)**, especially Handoff:** requires compatibility on the applications on both the macOS version and the iOS version. 
* **Smart card and ubiquitous terminals:** There was a company from the last century whose employees carried a smart card, not laptops, from/to meeting rooms. Terminals were available at their desks and in each meeting room, so one could plug in the card and get back to their desktop environment. This is great for demonstrations and team collaborations. Sadly, I could not find the original article I've read about this from.

### Present Status

Currently, I'm using a extra-portable ultrabook \(MacBook, 2015\) as my daily driver, plugging it into an adapter when I need a full-form desktop experience at home. The adapter connects my MacBook to a monitor, a full-size keyboard, a mouse, and a USB-A hub with one single cable. This is by far the most versatile form-switching experience I had, but it also comes with insufficiencies:

* MacBook has no touchscreen. I draw stuff and jot down notes quite often using my iPad. I wish they were one device.
* Handing off tasks between my iDevices and my laptop relies too heavily on cloud syncing. Apps that have very different iOS and macOS editions complicate the situation further.

### Requirements

Here's what I'd like to see in a solution:

* **Ability to continue work on different forms of devices.** Full-fledged 108-key keyboard + 35 inch monitor? Laptop that weighs under 2 lbs? Smartphone in your pockets? Yes please!
* **Ability to work on the same object**, not relying on transferring/syncing documents back and forth. This might imply "streaming": We can
  * stream video using technologies such as VNC \(which is slow & laggy but more compatible; I'm actually using VNC quite frequently\),
  * stream UI components such as windows using X-server \(which is less laggy, but more difficult to implement to different platforms\), or
  * stream text only using `ssh` + `tmux`, etc. I would really love to have GUI, though.
* Little sacrifice on performance.
* Little sacrifice on computational power.

### Possible Solutions

Here are a few possible solutions we can get started now:

* **Switch to Samsung**, I guess? At present, I believe this is the best way to solve the continuity problem between phone and desktop. I believe there's a good client app for remote desktop on Android, which could be used to connect us to a more powerful, immobile, device for computation-hungry tasks.
* Switch to Linux and start **forwarding all windows** through X?

## Safety of Data v.s. the Cost of Self-hosting

### Motivation

You want to keep your data safe \(reads: not leaked\). You can:

* Rely on external, encrypted storage, or
* host your own data, services, etc., if only you have the capacity to keep it reliable and safe.

Cost associated with self-hosting comes in different facets:

* Upfront cost:
  * Depends on your need, you might need to purchase dedicated device as your home server.
* Maintenance cost:
  * Utility cost: 
    * a decently powerful server can cost a lot on your electricity bill.
    * if you heavily rely on your own server, you probably need a fast Internet, which can be expensive.
  * You would probably want off-site backups regardless of self-hosting. This can be a headache to plan out.
  * Keep services **running**, **resilient** to disasters ****and **secure** from malicious activities.

### Requirements

I want my data and personal services to be:

* Available
  * able to access -- it should be up and running when I need it.
  * easy to access
    * Method of access: there should be POSIX-compliant and has an iOS app for that.
    * Simplicity: Authenticate and authorize me smartly.
  * fast to access -- a data vault that requires 10 min of retrieval for a phone number is not acceptable. 
* Coherent across copies -- that means local caches on each terminal device plus all redundant backups.
* Not be lost easily -- robust to hard disk failures, etc.
  * resilient to \(most likely natural\) disasters =&gt; calls for off-site backups, which might impact ease of access
  * secure from malicious activities =&gt; calls for authentication &  authorization mechanisms
* Not be leaked easily =&gt; calls for encryption

