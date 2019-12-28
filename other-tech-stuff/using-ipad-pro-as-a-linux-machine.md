---
description: Work in progress.
---

# Using iPad pro as a Linux machine

I bought my iPad mainly for note-taking during classes. Now that I have graduated, my iPad has been collecting dust ever since. Recently, I learned about this new open-source project that is essentially an Alpine Linux emulator on iOS, [iSH](https://github.com/tbodt/ish). I'm exploring possibilities of using iPad pro as a daily driver.

**Today, I still recommend against doing this.** This is due to the following disadvantages:

* iSH frequently freezes if I leave it open for around 20 min.
* The CPU does not have [MMX support](https://en.wikipedia.org/wiki/MMX_%28instruction_set%29). This means simple programs such as [`micro`](https://micro-editor.github.io/) cannot load in iSH.

Also, this article does not yet carry the topic too far. 

## Preparations

1. Install iSH.
2. [Set up SSH server](https://github.com/tbodt/ish/wiki/Running-an-SSH-server).
3. Do yourself a favor and make an `alias` in your `~/.profile`:

   `alias ipad="ssh -t root@192.168.0.106 'tmux a -t iPad || tmux new -s iPad'"`

## Things to do every time at boot

To prevent iSH from freezing when you switch to other apps:

```text
cat /dev/location > /dev/null &
```

To start SSH server:

```text
/usr/sbin/sshd
```

## Adding a `top`-like tool

One thing I would love to do is monitoring system performance. My usual go-to tool is `htop`, which -- sadly -- [does not yet work on iSH](https://github.com/tbodt/ish/issues/273). Therefore, I have to turn to an alternative, python-based tool called `ptop`.

1. Install dependencies:

   ```text
   apk add python3 gcc python3-dev musl-dev linux-headers
   ```

   \(Reason to install [`python3-dev`](https://github.com/pwndbg/pwndbg/issues/356#issuecomment-339048894), [`musl-dev`](https://stackoverflow.com/a/30873179/1147061), [`linux-headers`](https://github.com/mirage/mirage-block-unix/issues/45#issuecomment-196892988)\)

2. Install `ptop` with `pip`:

   ```text
   pip3 install ptop
   ```

Sadly, this also does not work.

