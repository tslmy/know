---
description: 'NOT for bypassing censorship, etc.'
---

# Setting Up My Own VPN for Work

**Setting up a VPN.** During my work, there are often times I need remote access to my computers behind firewalls and/or routers. I used to enjoy _LogMeIn Hamachi_ \(HMC\), but that app \(1\) appears to have died and \(2\) does not support latest macOS releases. For these two reasons, I'm switching to [ZeroTier One](https://www.zerotier.com/) \(0T1\). 0T1 allows for up to 100 connected devices per network, which is a huge plus compared to the 5-device limit on HMC.

{% hint style="info" %}
Just remember to toggle the checkbox under "Auth?" column in the network configuration page at [my.zerotier.com](https://my.zerotier.com). Wasted one minute on this.
{% endhint %}

**Graphic control.** It's never wise to rely on one type of network and call it for a day -- SSHing into another machine can be blocked by a public Wi-Fi network, and I've been there. Besides 0T1, I also set up a **RealVNC network** for 5 of my most frequently connected machines. Why 5, you ask? That's the limit for a free-tier network from RealVNC.

**Transferring files.** Transferring files shall better be achieved via `rsync` rather than relying on `scp`, which I enjoyed using for a couple of years. I've always heard of the powerful mightiness of `rsync`, but it's not until recently that I need to move thousands of ~1MB files from Philadelphia to China \(legally; it's important to point this out considering recent China-USA political trends\) that I discovered its ability to increase the performance by ten folds.

**Terminal session persistence.** I set up an alias for the following command:

```bash
ssh -tY USERNAME@MY.SERVER.edu -i ~/.ssh/KEYFILE_rsa 'tmux a -t MyServer || tmux new -s MyServer'
```

where `tmux a -t MyServer || tmux new -s MyServer` essentially attempts to attach to a _tmux session_ called "MyServer", and if it fails, a session of that name is created & attached.

In this way, I can restore my last terminal session with one command. Handy!

