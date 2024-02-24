---
layout: page
title: CHIRP Radio App (aka "Legacy DJ Database App")
permalink: /legacy_dj_app/
nav_order: 2
parent: Active Projects
---

# CHIRP Radio App (aka "Legacy DJ App")
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
* [Github Repo](https://github.com/chirpradio/chirpradio)
* [Production Instance](https://chirpradio.appspot.com/auth/hello?redirect=/)

## What is the CHIRP Radio App?
The CHIRP Radio app (aka "Legacy DJ Database App") is used by all CHIRP DJs and Music Department staff to perform essential tasks related to our music metadata library, including vital on-air tasks. It is currently in the process of being replaced by [NextUp](nextup.md).

Current Functionality Includes:
* CRUD, search (buggy) and very rudimentary tagging/sorting functionality for album metadata in the music database
* Save albums to personalized crates (buggy)
* Push song metadata to the on-air playlist
* View DJ Traffic Log (the schedule of promos and station information that must be read on-air by the DJs)
* Admin portal to update the traffic log

## Tech Specs
The CHIRP Radio App is written in Python 2.7 using Django 1.2.5. The app is hosted on Google Cloud.
A recording from our 2024 meeting "Legacy DJ App 101 and Demo" can be found in Slack [here](https://chirpdev.slack.com/archives/C01GSPCEDMK/p1705978509222069).

## How To Contribute
* This app is not currently taking feature requests, since it's being replaced.
* Instructions for setting up for local development can be found [here](https://chirpradio.readthedocs.io/en/latest/index.html).
* Check out the backlog in [Trello](https://trello.com/b/B1L4W9A9/dev-projects) for a list of unassigned tasks tagged "Legacy" that are waiting to be worked on.