---
description: 'Describes how I take, store, and edit various notes.'
---

# 📝 Organizing Notes

![https://unsplash.com/photos/5bYxXawHOQg](../.gitbook/assets/image%20%288%29%20%281%29.png)

## Requirements

Data should be easily updatable \(this is the input\) & easily accessible \(this is the output\). Currently, my notes are stored on a GitHub repo. That means:

### Easily Accessible

This can be broken into 2 scenarios, depending on sensitivity of data.

#### Insensible notes should be searchable online

To have them **easily accessible**, I want them to be full-text-indexed and searchable.

* I want the insensitive data to be searchable **online**, so that I can have access to my notes without access to my computers.
  * **Existing solutions**: Are there any? What are they? How good are they?
    * GitBook \(Figure 1\)
      * pros:
        * Has **URL** form -- e.g. [https://tslmy.gitbook.io/k/?q=typora](https://tslmy.gitbook.io/k/?q=typora) would give you search results in my Wiki with the keyword "typora".
      * cons:
        * Search is dynamically loaded -- slow to render.
        * An online service -- does not work offline.
    * **GitHub** \(Figure 2\)
      * pros:
        * Has **URL** form -- e.g. [https://github.com/tslmy/know/search?q=typora&unscoped\_q=typora](https://github.com/tslmy/know/search?q=typora&unscoped_q=typora) would give you search results in my Wiki with the keyword "typora".
        * Statistically loaded -- renders faster than GitBook.
      * cons:
        * An **online** service -- does not work offline.

![Figure 1: Search UI on GitBook](../.gitbook/assets/image%20%2812%29.png)

![Figure 2: Search UI on GitHub](../.gitbook/assets/image%20%282%29.png)

### 

#### Sensitive data to be kept **offline** and still searchable

* Existing solutions: Are there any? What are they? How good are they?
  * OneNote / EverNote / Notability
    * pros
      * robust functionalities
    * cons
      * walled gardens
  * macOS Spotlight
    * pros
      * really easy access -- integrated with the OS
    * cons
      * does not support notes in walled gardens \(not even Zotero references\)
      * not portable -- different OSes offer incoherent experiences. This actually resembles the "walled garden" critique from the previous option.
  * command-line tools
    * resources
      * features comparison of several CLI regexp search tools: [here](https://beyondgrep.com/feature-comparison/)
      * speed comparison of ~~~~: [here](https://github.com/BurntSushi/ripgrep#quick-examples-comparing-tools)
    * Looks like the best choice is [`ripgrep`](https://github.com/BurntSushi/ripgrep) . 
      * Need to do:
        * auto-exporting data from all sources to plain text and save locally.
      * pros
      * cons

### Easily Updatable

The best option for now I've found is GitBook. It's got a decent webUI editor \(although it has a list of quirks -- see below -- and is slow on an old computer\), syncs to your GitHub, and its syntax is interoperable with Markdown.

List of quirks of GitBook:

* aggressive undoing
* when you copy something from a list and paste it somewhere else, the whole list indention builds up again. e.g., if you copied some text from a 3rd-level nested list and past it on a 2nd, you will get a 5th-level result.

_TODO: This section needs expansion._

## Solutions

Stick with GitBook for adding & updating public notes. TODO:

* Find a way to auto-update local copy of GitBook notes.
* Validate that I can conveniently search locally all my notes \(that means private notes as local `md` files + public notes from GitBook\) with `ripgrep`. 
* Add a custom search engine to my Chrome that searches the GitHub repo directly.

## \(Deprecated\) How Notes & Writings Can Be Categorized

![Classifications of my writings &amp; notes, and where to put them.](../.gitbook/assets/image%20%288%29%20%282%29.png)

| Type | Updatable? | How Refined? | Can Made Public? | How valuable to others? |
| :--- | :--- | :--- | :--- | :--- |
| Diary | Never | -2 | N | 0 |
| Personal Journal | Daily | -3 | N | 0 |
| Credentials / Passwords | At times | N/A | N | 3 |
| Academic papers | Never | 3 | Y | 3 |
| Various Essays | Never | 2 | Y | 2 |
| Quick Notes | Seldom | -1 | N | 1 |
| Reviews / Summaries | Maybe | 1 | Y | 2 |
| Web Clippings | Never | N/A | N/A | 1 |
| Translations / Transcripts | Never | 3 | Y | 2 |

* `N/A` means "not my own work, thus does not apply."
* Numbers are on a 7-point scale.

### How I Allocate Apps to Different Note-taking Purposes

Crossed-outs are what I used to use but moved away from \(due to death of product, etc.\).

### Note-taking and Storage

* Course notes / meeting notes that better be hand-drawn: **Notability** \(iPad\)
* Diary, personal journal: ~~Day One~~ **OneNote**
* Course reviews and summaries: ~~Evernote~~ **Notability**, course-specific **folders**, and -- in cases that the notes may be shared -- my [**academic website**](http://seas.upenn.edu/~myli). 
* Scribbles, jots, etc.: A folder full of plain text/markdown files.
  * Synced with ~~Simplenote~~ Dropbox.
  * Read with ~~Notational Velocity, nvALT~~ **fsNotes**.

### Editors and Word Processors

* Coding/writing temporarily - **Sublime Text**
* Quickly generating PDFs from Markdown - ~~Mou~~ **Typora**
* Academic writing \(essay, things with a formula/equation, etc.\) - **LyX**
* For language-checking - **Hemingway Editor + SlickWrite**
* Mind-mapping - **MindNode** 
* \(Math stuff excluded\)
* \(Office suites excluded\)
* \(Reminder and Calendar excluded\)
* \(Rare-format editors excluded\)

### ~~Cloud Storages~~

* ~~Mobile Syncing - Dropbox~~
* ~~Google Office - Google Drive~~
* ~~Microsoft Office - OneDrive~~
* ~~Backup - Box~~

