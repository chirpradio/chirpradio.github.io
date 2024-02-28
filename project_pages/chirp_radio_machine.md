---
layout: page
title: CHIRP Radio Machine
permalink: /chirp_radio_machine/
nav_order: 4
parent: Active Projects
---

# CHIRP Radio Machine
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# The Basics

## Quick Links
* [Github Repo](https://github.com/chirpradio/chirpradio-machine)

## What is CHIRP Radio Machine?
The CHIRP Radio Machine is a set of support scripts that were originally created to be used with the [CHIRP Radio App (aka "Legacy DJ Database App")](legacy_dj_ap.md). Currently, the main functionality it is still being used for is importing new music. An import will add the actual music files to Traktor (software on an in-studio computer used for playing music) and add the corresponding album metadata to the music library database used by both the Legacy DJ App and its successor, NextUp. The import is run by the Music Department on a regular basis.

## Tech Specs
The Stream  Archiver is written in Python 2.7, and runs from Google App Engine using Virtualenv. Imports are run by SSH-ing into a server in the studio and running scripts under the musiclib user.

# How To Contribute
* Check out the backlog in [Trello](https://trello.com/b/B1L4W9A9/dev-projects) for a list of unassigned tasks tagged "Stream archiver" that are waiting to be worked on.
* Instructions for setting up and running the scripts can be found [here](https://github.com/chirpradio/chirpradio-machine)
* You may also need a server admin to grant you permissions to run scripts under the musiclib user on the studio server.