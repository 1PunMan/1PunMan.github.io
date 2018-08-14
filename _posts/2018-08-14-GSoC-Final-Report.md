---
title: "GSoC'18 - Final Report"
excerpt: "Conclusion"
header:
  teaser: "/assets/gnome.png"

tags:
    GNOME
    GSoC
    grilo
    grilo-plugins
    thegamesdb
---

As GSoC'18 ends, I'm writing this final report as a summary of the current state of the project.

## Summary

My project can be majorly divided into the following subtasks. Deatils about my project and subtasks can be found here- [1](https://1punman.github.io/GSoC-Self-Registering-Keys/), [2](https://1punman.github.io/GSoC-Segregated-Views/), [3](https://1punman.github.io/GSoC-Description-View/).

### Fetching metadata to Games

Currently Games never made use of any metadata provided by thegamesdb. My first task was to enable Games to fetch this metadata. This is the core of my projct as all the other tasks are dependent on this one. My changes for this have already been pushed to master.

### Allow grilo to set values for non-registered keys

My following task was to add missing Grl KeyIDs to grilo in order to succesfully fetch them to Games, but adding too many KeyIDs to core grilo was not suitable. I wrote a new grio API to succesfully register and set data to non-registered keys which took a lot more time than expected. The first goal to be met in order to achieve that was allowing grilo to set values for non-registered keys. My patches for this have already been pushed to master.

### Allow Lua plugins to self register keys

In order to fetch all of metadata to games, the only task remaining was allowing lua sources to register keys by themselves. This would allow anyone to use any key for lua based sources without having to worry about adding those keys as core system keys. This has already been pushed to master.

### Segregating-view

Here I make the first use of the metadata I added to Games. Two new views, developers view and platforms view were added to Games which display games grouped by a particular developer or platform respectively. This was the most enjoyable task to work on as this provided a much needed UI upgrade to Games. You can try this as this has already been merged to master.

### Description-view

This made use of all the remaining metadata that I was fetching to Games. Description view displays all of the game metadata like
  * Description
  * Cover
  * Title
  * Rating
  * Developer
  * Publisher
  * Genre
  * Coop
  * Release Date
  * Players

This is almost complete, it can be built and used through my patches. Some minor fixes and a review are required to get this merged to master.

### Bugs

I fixed a few bugs I encountered along the way of my project. All of these bug fixes were pushed to master.

### Tasks left

Some of the tasks I had originally planned took a lot more time than expected. My last task was to add stats to games that track and store your overall game statistics. I've already began working on this and will get it merged after thoroughly getting it reviewed by my mentors.


## Work Product

I've uploaded all my current patches to a drive [folder](https://drive.google.com/drive/folders/1EmjR-ZIzWQMSGO2ZW2WfEylFpKcGUQWC) for easy availability. Additionally all my patches are also avaialable on Gitlab.


## A few words

I had a wonderful time contributing to GNOME since I started this February. The amazing community and even more amazing mentors helped me learn new things and guided me all along the way which I would like to thank them for. I will surely keep contributing to GNOME.

Special thanks to [Adrien](https://wiki.gnome.org/AdrienPlazas), [theawless](https://wiki.gnome.org/AbhinavSingh) and [exalm](https://gitlab.gnome.org/exalm). Thank you for making my summers super exciting.