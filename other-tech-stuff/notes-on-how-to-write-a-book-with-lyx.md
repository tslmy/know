# Notes on how to write a book with LyX

![](../.gitbook/assets/image%20%284%29.png)

## Setup

I use Zotero with [the LyZ plugin](https://github.com/willsALMANJ/lyz) for managing resources that need to be inserted into my books. Such resources include references and CC0 images. 

## How to render...

### ... Chinese Characters

Change these settings:

* In Document &gt; Settings... &gt; Document Class &gt; Document Class, choose "Chinese Book \(CTeX\)".
* In Document &gt; Settings... &gt; Language &gt; Language, choose "Chinese".
* In Document &gt; Settings... &gt; Formats &gt; Output Format &gt; Default output format, choose "PDF \(XeTeX\)". XeTeX, in my experience, is the best renderer.

#### About Fonts

Assuming you have Homebrew installed, you can install Chinese fonts that is freely available for publications, such as [Source Han Serif](https://source.typekit.com/source-han-serif/). First, you need to add the tap:

```text
brew tap homebrew/cask-fonts
```

Now, install [Source Han Serif](https://source.typekit.com/source-han-serif/):

```text
brew cask install font-source-han-serif
```

Finally, you can change more settings now. In Document &gt; Settings... &gt; Fonts, tick "Use non-TeX fonts". Choose "Source Han Serif" in "Roman". I also chose the same font for "Sans Serif", but you probably should not.

### ... Emojis

To render Emojis, I use [`xelatex-emoji`](https://github.com/mreq/xelatex-emoji). In Document &gt; Settings... &gt; LaTeX Preamble, add:

```text
\usepackage{xelatexemoji/xelatexemoji}
```



