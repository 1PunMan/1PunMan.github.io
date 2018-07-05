---
title: "Segregating views"
excerpt: "4th June - 25th June"
header: 
  teaser: "/assets/gnome.png"

tags:
  - GNOME
  - GSoC
  - GNOME Games
  - Grilo
---

In my last blog [post](https://1punman.github.io/GSoC-Self-Registering-Keys/) I talked about how to add self registering keys to lua based sources and segregating views. Now I was finally free to add and use any keys I wanted to `thegamesdb` for fetching and using that metadata. Here's how I used the newly added feature to grilo.

## 4th June - 25th June

As I had already added keys like `description`, `rating`, `developer` and `publisher`, I began by adding all the following remaining keys to `thegamesdb` and GNOME Games.
  * `release date`
  * `coop`
  * `players`
  * `genre`

These keys will be later used to display game metadata as `description view`.

### What happened to segregating views?

For a long time now Games has had a very basic UI, displaying only a collection of games. Having already had added the `developer` key to Games, I chose to add a `developer view`, displaying collection of games by developer. Along with the `developer view` a `platform view` was also added to display collection of games by platforms. A `GtkStackSwitcher` was added to the header bat to easily navigate between these views.

### Developer view

<figure>
	<a href="/assets/images/Developer_1.png"><img src="/assets/images/Developer_1.png"></a>
</figure>

<figure>
	<a href="/assets/images/Developer_2.png"><img src="/assets/images/Developer_2.png"></a>
</figure>

The games which do not use Grilo to fetch their metadata or the games for which the `developer` wasn't available were assigned an "Unknown" developer.


### Platform view

<figure>
	<a href="/assets/images/Platform_1.png"><img src="/assets/images/Platform_1.png"></a>
</figure>

<figure>
	<a href="/assets/images/Platform_2.png"><img src="/assets/images/Platform_2.png"></a>
</figure>

Game covers aren't currently visible as `thegamesdb` have switched to a new API. I'll soon be updating `grl-thegamesdb` to use this newly updated API.

I've already started working on `description view` mentioned above, and will be updating you all soon on it.

Cheers!