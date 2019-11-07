---
description: For archival purposes only; I moved back to macOS eventually.
---

# 🐧 Switching From macOS To Linux

My workload has finally escalated to a stage where my MacBook can't suffice. Unfortunately, as an international student, I found my budget suffocatingly tight when it comes to purchasing another computer -- a third Mac is definitely out of the question. In fact, another laptop also won't be ideal -- I could really use a more performance-focused machine at home that I could just SSH into when needed. After some digging, I built my first full-size desktop PC in North America. It is time to incorporate it to the Apple ecosystem that I'm already familiar with.

### Hardware Specification And Budget Overview

My hardware specification is as follows:

* **Optiplex 7010 MT**: A decent refurb I won from an eBay bidding with USD$70.
* **Nvidia GeForce GTX 460**: A little piece of impulse shopping that I got for USD$30.
* **Patriot 4GB DDR3 1600 RAM** x 2: Because the stock 4GB memory just won't suffice. USD$40.
* **Kingston SSDNow 30GB**: A cheap piece of Solid State Drive that I got for USD$10.
* **DELL S2209W Monitor**: A decent 1920x1080 display unit that I got from CeX before it ceased business from the US. I really liked them. $15.
* **Some cables and adapters**: Another USD$14.

That's a total of USD$180 \(~CAD$230 or CNY$1,145\). Not a bad deal!

#### Sidenote On The Graphics Card

Initially, I wanted to build a Hackintosh. The integrated graphics chipset \(namely Intel HD2500\) supports only one VGA output, a port long abandoned by macOS. This made an external graphics card a must. Although I never ended up actually installing the macOS -- which would probably be illegal -- on this machine, this piece of GeForce GTX 460 stayed.

To power this thing up, I had to purchase two SATA-to-6 pin PICe power adapters, which came in a pack of 3 on Amazon for USD$8. I also had to buy a DVI cable for another USD$7. If you decide to stick with the integrated GPU, you would save a total of USD$44 in comparison.

Lastly, you will need [this driver](http://www.nvidia.com/Download/driverResults.aspx/104284/en-us) for maximum performance.

### Operating System And Terminal Lift-Up

#### Choosing The Right Distro

The Dell Optiplex came with a Windows 10 Pro license. After using macOS as my main operating system for &gt;7 years, coming back to Windows was really an astonishing experience -- especially, Microsoft Account integration is way smarter than an iCloud account, the latter of which basically requires you to log in to each app \(FaceTime, App Store, Messages, etc.\) separately. However, I had to say goodbye to Windows again in favor of a \*nix distribution. Yes, I had tested out Linux Subsystem -- it's just not THAT well integrated.

When preparing for a [tutorial for UPenn SEAS students](https://www.seas.upenn.edu/~myli/CourseNotes/CIS545/HowToSetUpDockerAtSEAS.md), I have compared multiple linux distros, finally coming to the conclusion that Debian is probably the best balance point between minimality \(especially important, considering the size of my SSD\) and stability \(Debian to Linux is what [DongLaiShun](https://www.tripadvisor.com/Restaurant_Review-g294212-d1158029-Reviews-Dong_lai_Shun_Restaurant-Beijing.html) is to [Peking Roasted Ducks](https://en.wikipedia.org/wiki/Peking_duck)\). I assume you know how to install a Debian. If not, Google.

#### Enabling `sudo`

Depending on whether you installed certain Window Manager, `sudo` may or may not be already set up for you. You should probably fix this now:

```text
su # and then enter root passwordapt-get install sudousermod -aG sudo [YOUR LINUX USERNAME HERE]exit # back to normal user
```

After reboot, you should have `sudo` access just like you usually would.

#### Customizing The Terminal

I personally prefer `zsh` and its plugin manager `oh-my-zsh`. I had them installed in every Mac I own, so it's already an essential part to build a Mac-like experience for me:

```bash
sudo apt install zsh git #install zsh and gitsh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" # install oh-my-zsh
```

### Syncing Preferences From macOS to Linux

Install [Dropbox](https://www.dropbox.com/install-linux) from its website, then install `mackup` via:

```text
pip install --upgrade mackup
```

Assuming you have instructed `mackup` to backup your settings from a Mac, you can now restore them to your new Linux box by issuing:

```text
mackup restore
```

Your settings should be put back to where they are on your Mac and kept sync, although I'm not sure how many of those settings you can make use of on a Linux machine.

### File Access

#### Mount Time Capsule Volumes Onto Linux

**via SMB — can be automatically mounted**

Assuming your Time Capsule is at `192.168.1.1`, having two volumes shared, `Capsule` and `Backup`, add these lines to your `/etc/fstab`:

```text
//192.168.1.1/Capsule /mnt/capsule cifs pass=[TIME CAPSULE PASSWORD HERE],file_mode=0777,dir_mode=0777,sec=ntlm 0 0//192.168.1.1/Backup /mnt/backup cifs pass=[TIME CAPSULE PASSWORD HERE],file_mode=0777,dir_mode=0777,sec=ntlm 0 0
```

Remember to install `cifs`:

```bash
sudo apt-get install cifs-utils
```

and make two new empty folders as mounting points:

```bash
sudo mkdir -p /mnt/capsulesudo mkdir -p /mnt/backup
```

**via AFP — better compatibility with Time Capsule**

First, install dependencies:

```text
sudo apt-get install g++ libfuse-dev libreadline-dev libncurses5-dev git
```

If conflict on `libselinux-dev` occurs, use `aptitude`:

```text
sudo apt-get install aptitudesudo aptitude install libselinux-dev# use `.` key to natigate to a Solution that installs `libselinux-dev`. Accept it.
```

Now actually install

```text
sudo apt-get install g++ libgcrypt-dev libgmp3-dev libfuse-dev libreadline-dev libncurses5-dev gitgit clone https://github.com/simonvetter/afpfs-ngcd afpfs-ng/./configure --enable-gcrypt=/usr/lib && make && sudo make install && echo 'done!'sudo ldconfig # update the shared library cachesudo mkdir /mnt/capsule_afpsudo chmod 777 /mnt/capsule_afpmount_afp "afp://me:[TIME CAPSULE PASSWORD HERE]@192.168.1.1/Capsule" /mnt/capsule_afp # Time Capsule uses the dummy username `me` for AFP access with Volume .
```

#### Share Folders From And To A Mac

**Access Shard Folder On A Mac From Linux**

If you want your Linux machine to automatically mount some shared volumes on other Mac computer, this `fstab` file is the go-to place. For example:

```text
//my-macbook.local/lmy /mnt/mac-home cifs credentials=/home/lmy/.smbcredentials,iocharset=utf8,sec=ntlm,nounix,sec=ntlmssp 0 0
```

Notice that I used the `credentials` option here for better security. The `/home/lmy/.smbcredentials` is of the following format:

```text
username=[UNIX USERNAME ON YOUR MAC]password=[PASSWORD ON YOUR MAC]
```

Remember to restrict access to this file by `chmod 600 ~/.smbcredentials`.

**Access Shard Folder On Linux From A Mac**

On your Linux, install `netatalk` via `sudo apt install netatalk`. After installation, you can see your Linux machine right away from the "Shared" section in the Finder's Sidebar on any Mac in your local network.

Add these lines to `/etc/netatalk/`:

```text
/mnt/capsule      options:tm      "Capsule via SMB"/mnt/backup             "USB HDD via SMB"
```

Then restart the `netatalk` service:

```text
sudo /etc/init.d/netatalk restart
```

If you want to access your Linux PC even when you are away from home, see the following section:

**Ensure Mutual Access By Setting Up A Small VPN Of Your Own**

Install [LogMeIn Hamachi](https://www.vpn.net/linux) on your Linux machine and your MacBook, too. While Hamachi is easy to configure on a Mac, under Linux you will need to user terminal:

```bash
sudo hamachi login [YOUR LOG-ME-IN EMAIL]
```

Now wherever your MacBook is, as long it has Internet Access \(One possible scenario: I usually leave my MacBook at work and want to access its file at home\), you can use the mounted folders just like the MacBook were home.

_As of May 2018, if your Hamachi doesn't work \(technically, if you have libc6 of a version higher than 2.25\), use "Hamachi for Linux BETA versions with glibc 2.26" instead of the usual one._

### SysAdmin Stuff

#### Enable Tmux

Install [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm#installation).

### Application Selection

#### Cross-Platform Apps That Resembles A Mac Experience

These apps here provides nearly-identical expriences across platforms:

* Google Chrome
* Typora
* Sublime Text 3

#### Linux Alternatives To Mac Apps

* ~~**Back In Time**~~ **DeJa Dup**: Time Machine alternative. If you come from Wndows, this is like File Versions. You should have completed the Auto-Mount Time Machine Volumes section above before deploying this.
* **Unsplashy**, or other gadget that periodically changes wallpaper from Unsplash for you: See [this](http://youness.net/linux/set-random-wallpapers-unsplash-com-ubuntu) fantastic article.
* [**Albert**](https://software.opensuse.org/download.html?project=home:manuelschneid3r&package=albert): Alternative to Spotlight.

### Developer Tools

I use Anaconda \(Miniconda, actually\) more often than I brush my teeth. After downloading one from [this website](https://conda.io/miniconda.html), install by `sh Miniconda3-latest-Linux-x86_64.sh`.

#### Node.JS

```text
# Install NVM:curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

Add these lines to `~/.zshrc`:

```text
export NVM_DIR="$HOME/.nvm"[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

Install Node:

```text
nvm install node
```

#### System Monitoring

I'm using [linux-dash](https://github.com/afaqurk/linux-dash):

```text
## 1. clone the repogit clone --depth 1 https://github.com/afaqurk/linux-dash.git## 2. go to the cloned directorycd linux-dash/app/server## install dependenciesnpm install --production## start linux-dash (on port 80 by default; may require sudo)## You may change this with the `LINUX_DASH_SERVER_PORT` environment variable (eg. `LINUX_DASH_SERVER_PORT=8080 node server`)## or provide a --port flag to the command belowLINUX_DASH_SERVER_PORT=8864 node index.js
```

or `htop`:

```text
sudo apt install htop
```

