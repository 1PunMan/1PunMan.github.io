---
title: "Description view"
excerpt: "26th June - 14th July"
header: 
  teaser: "/assets/gnome.png"

tags:
  - GNOME
  - GSoC
  - GNOME Games
  - Grilo
---

For a while now I've been hacking away at Games to add metadata objects fetched using `grl-thegamesdb`, and till now only `developer` metadata object was used, for showing a `developers view`. All of this was done in order to add a `description view` to Games, displaying metadata for games. Here's what I've acheived.

## 26th June - 14th July

After discussing in depth the design concept for `description view` with [aplazas](https://wiki.gnome.org/AdrienPlazas), exalm and [theawless](https://wiki.gnome.org/AbhinavSingh) it was decided that the new view will be added as a `GtkStack` along with the already present `game view`. A `GtkStackSwitcher` was added to the header bar to easily navigate between the two views.

### How does it look?

<figure>
	<a href="/assets/images/Game_1.png"><img src="/assets/images/Game_1.png"></a>
</figure>

Something like this.

Now, coming to the `description view` itself, along with displaying metadata objects like `Developer`, `Publisher`, `Co-op`, `Release Date`, `Genre` as `GtkLabels`, `Cover` is being displayed in a thumbnail view with the game's title placed just below the thumbnail as a `GtkLabel`, additionally a game's `Rating` is rounded off and shown as a Star Rating. `Description` is shown in a `GtkScrolledWindow` placed just adjacent to the thumbnail.

### Description view

<figure>
	<a href="/assets/images/Description_1.png"><img src="/assets/images/Description_1.png"></a>
</figure>

<figure>
	<a href="/assets/images/Description_2.png"><img src="/assets/images/Description_2.png"></a>
</figure>

### What's remaining?

Currently the only information being displayed is what we fetch from `thegamesdb`, my next task will be to add local stats to Games and displaying them in the `description view`. These stats will include
  * `Current play duration`
  * `No. of times played`
  * `No. of times finished`
  * `Total hours played`

Finally a `Finished` button will be added to the `description view` so that a user can mark an end for the game.

In my previous blog [post](https://1punman.github.io/GSoC-Segregated-Views/), I mentioned how the `thegamesb` API was broken. For the time being it has been switched to the old API and will be updated in the future once the new API has stabilized.
