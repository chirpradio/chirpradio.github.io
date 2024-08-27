---
layout: page
title: Stream Archiver
permalink: /stream_archiver/
nav_order: 6
parent: Active Projects
---

# Stream Archiver
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
* [Github Repo](https://github.com/chirpradio/stream-archiver)

## What is the Stream Archiver?
The Stream Archiver records the live stream of our station and writes the data to MP3s. It then returns a player for the latest two recordings of a DJ's show, which are embedded on each DJ's page on our website for users to listen to. The biggest pain point with this process is that it is entirely based on the date and time of the recorded stream, so DJs who are substituting for another DJ's show will end up archived on the page of the DJ whose time slot they were recorded in.

## Tech Specs
The Stream  Archiver is split into two parts: Recorder and Player. The Recorder is a Python script run by cron jobs, both of which are built into a Docker image and deployed to Google Compute Engine. The resulting MP3 files are stored in a Google Cloud Storage bucket. The bucket is configured in the console to delete any files with an age greater than 14 days. The player is a minimal Express app deployed as a Google Cloud Function.

# How To Contribute
* Check out the backlog in [Trello](https://trello.com/b/B1L4W9A9/dev-projects) for a list of unassigned tasks tagged "Stream archiver" that are waiting to be worked on.
* Minimal instructions for testing and deploying can be found [here](https://github.com/chirpradio/stream-archiver/blob/main/recorder/README.md) for the Recorder and [here](https://github.com/chirpradio/stream-archiver/blob/main/player/README.md) for the Player.
* You may also need access to Google Compute Engine, where the cron jobs run, and our Google Cloud Storage Bucket, where the MP3s are stored.