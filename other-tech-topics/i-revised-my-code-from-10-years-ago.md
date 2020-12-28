---
description: 'https://github.com/tslmy/t.t.t'
---

# I revised my code from 10 years ago

Around 10 years ago, when I had just picked up coding as a hobby, I taught myself PHP \(I was young\). Using PHP and a few nights after school, I made a blog engine and never updated it since.

The engine was named [_t.t.t_](https://github.com/tslmy/t.t.t), an acronym for my old blog, `the.tslimi.tk`. Apparently, it has lost this origin as I moved on to other blogging platforms. Feel free to interpret it any way you like.

_t.t.t_ reads a directory of markdown files as posts. It doesn't use database simply because I didn't know how to use one. Although there was an experimental composing interface, it was not access-controlled, and you mainly post a article by uploading a new file. The PHP code renders each `txt` file into `HTML` and saves the HTML version in a `cache/` folder, where the code would look up first.

Over this holiday weekend, I was learning about containerization. As an exercise, I thought it would be cool to containerize a project of my own. The project of choice should be small in size so that it's manageable and won't dwarf the containerization part, and it should ideally be a web service. Naturally, I thought of _t.t.t_, which only had &lt;1,000 lines of code and is a server.

While I was inspecting the code, I identified some low-hanging fruits that I could probably smooth out before getting into business, such as applying [early returns](https://news.ycombinator.com/item?id=16678209) and [prettifying](https://github.com/FriendsOfPHP/PHP-CS-Fixer) the code. The cleaning job, however, took me 10.5 work hours.

## Adapting a package manager

_t.t.t_ used to have all its dependencies saved as part of the source code. This brought surprising longevity to the project: I downloaded the code from GitHub, executed `php` in the decompressed directory, and it just works. Compare it with the last blog engine I wrote 5 years ago, _GitPub_: _GitPub_ used external services for packages, namely [Eager](https://eager.io/). As the company was acquired by CloudFlare, _GitPub_ had long stopped working years since. Now I see the benefit of using a [monorepo](https://en.wikipedia.org/wiki/Monorepo).

Back then, I didn't use any package manager simply because I didn't know such technology existed. A package manager helps your repo to contain only the code you write. This has benefits in terms of storage space and upgradability. Naturally, the first update I made to _t.t.t_ was migrating all its dependencies to a package manager. In the case of PHP, I had to learn about a new tool, namely [Composer](https://getcomposer.org/).

Now that I have a package manager, the next thing I did was replacing some functionalities that I wrote myself with battle-tested packages available online. These include:

* Pagination: `Pagerfanta`. This saved `t.t.t` ~150 lines of code, which is substantial considering the whole repo contained only ~450 LoC when I made this switch.
* CSS: Although I loved my minimalist, [neumorphic](https://medium.com/@artofofiare/neumorphism-the-right-way-a-2020-design-trend-386e6a09040a) design, nowadays I prefer semantic HTML and responsive CSS more. For this reason, I replaced my hand-written stylesheets with [mvp.css](https://andybrewer.github.io/mvp/). 
  * Isn't it interesting how I skipped Bootstrap, which I had heavily used in several of my projects such as [_ckwatson_](https://github.com/ckwatson/web_gui)?
  * By the way, my [homepage](http://myli.page/) also uses this CSS framework.
* Instead of using one `favicon.ico` file of `mspaint.exe` quality, the blog engine is now using a whole set of favicon files generated from [favicon.io](https://favicon.io/).

## Removing stuff

Due to the switch in CSS, there are a couple of features that no longer fitted into the new design: The semi-transparent header images in the index page, and the "Quick Access" dropdown menu. I had to remove these features. Their removal led to further reductions in the code: _t.t.t_ no longer hides files whose names begin with `_`, and it no longer depends on jQuery \(hooray\).

It \[felt good\]\[fg\] to see that the code complexity dropped when I was removing the header image feature. Therefore, I continued to remove more:

* The `_intro.txt` behavior has been removed to reduce complexity in the rendering process. This means _t.t.t_ no longer hides `_`-started files.
* The caching behavior has been removed. It was a fun experience to have implemented my own caching mechanism, but the complexity-efficiency trade-off was just not paying off.

In addition \(or, should I say "reduction"?\), undocumented behavior \(such as RSS support and an alternative list view\) and dependencies that stopped working themselves \(such as the social sharing buttons\) were also removed.

## Containerization

Also, since it's 2020, containerization is great:

* Dockerfile
* Docker Compose
* Heroku Procfile \(and one-click deploy button\)
* Kubernetes manifest

It might sound like an overkill for a 300-LoC project, but isn't that the whole point of revising _t.t.t_?

## To-dos

These things sounds quite interesting:

* [ ] add unit tests.
* [ ] use [`social-links/social-links`](https://packagist.org/packages/social-links/social-links) as a replacement for _JiaThis_.
* [ ] make the docker/kubernetes setup work with a volume mapping.



