---
layout: default
title: Endless Sky - Architecture
---
## Introduction

Endless Sky consists of an executable program written in C++, data files that describe the game universe in a structured text format, and resource files (images and sounds). This document describes the architecture of the C++ program, to help developers to understand how the code works and where to find the code for a given aspect of the game.

Content creators who are only interested in modifying the text files should refer to the [wiki](https://github.com/endless-sky/endless-sky/wiki) rather than this document, unless they are looking for implementation details that are too low-level to be mentioned in the wiki.

## Documentation overview

Endless Sky uses something similar to a [Model - View - Presenter](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter) architecture, consisting of a Model (the underlying simulation of the game universe), a Presenter (the layouts for individual user interfaces and the code for deciding what to draw), and a View (the actual code for rendering graphics and playing sounds). The underlying Model consists of three different layers:

* The [game data](data.html) includes systems and planets, ship types and outfits, and templates for missions that can be offered. Some aspects of the universe can change in response to a scripted event. These changes only take place when a day passes in game, which happens when the player enters a new star system or departs from a planet.

* The [player information](player.html) includes what assets the player owns, what missions they have accepted, and what choices they have made. The player’s state is loaded from a saved game file and changes in response to actions that the player takes.

* The [game engine](engine.html) tracks the ships and projectiles that are currently “in flight,” including applying the AI to ships and tracking projectile collisions. The engine’s state updates 60 times per second.

The [user interface code](interface.html) includes the main menu and the panels that show information to the player or allow them to perform different actions on a planet. It also includes classes that allow the placement of certain UI elements to be specified in an `interface` data element.

The [graphics and audio](resources.html) code allows drawing sprites, rendering vector graphics (lines, circles, pointers, etc.), and playing sounds. Most of the image and sound resources are loaded when the game first starts up, but very large resources (landscape graphics and ambient sounds) are loaded dynamically as needed.

Some basic [utility code](utilities.html) is used by many of the components listed above. That includes classes representing points, angles, and rectangles, and functions for reading and writing files.

Each of the six components linked above is described in detail in one chapter of this design document. Each chapter starts with an overview, followed by implementation details for each sub-component.

