---
layout: page
title: Nite Owl
permalink: /nite_owl/
nav_order: 5
parent: Active Projects
---

# Nite Owl
{: .no_toc}

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
* [Github Repo](https://github.com/chirpradio/cloud-functions)
* Slack Channel: [#proj-nite-owl](https://chirpdev.slack.com/archives/C01GW3BRV5H)
* [StationPlaylist Studio](https://stationplaylist.com/studio.html)

## What is Nite Owl?

Nite Owl is the overnight programming at CHIRP Radio. In these overnight hours, we rely on the software StationPlaylist to play tracks rather than live DJs. Where our DJs use the playlist tracker to enter playlist information, we need a different method to capture tracks played by this overnight automation software. That is the main purpose of this probject.

StationPlaylist has the option to transmit now playing information to a target URL which we can then use to write information to the CHIRP playlist tracker.

## Tech Specs

The implementation of this functionality is a NodeJS application which is the target for a Google Cloud Function triggered by HTTP. For a basic overview of this approach, see here: [Cloud Functions: Write HTTP Functions](https://cloud.google.com/functions/docs/writing/write-http-functions)

# How to Contribute
TODO

# Developer Documentation

## StationPlaylist Configuration

Our ability to capture track information is supported by StationPlaylist's Now Playing configuration. This is available by navigating to _View->Options_ and then navigating within the resulting menus as follows:

1. Now Playing
2. Stream Metadata
3. Output via HTTP request

![Station Playlist Configuration](/assets/images/nite_owl-stationplaylistconfig.png)

The main area of concern for us is #3 from above. What we need to enter here is a templated URL that will convey information to the HTTP-triggered Google Cloud Function.

These are the parameters that are relevant to us:

| Parameter | Description  |
|:----------|:-------------|
| %A        | Album Artist |
| %t        | Song title   |
| %T        | Album title  |
| %L        | Label        |

As it applies to the request URL that will reach our HTTP-triggered cloud function, the query parameters in our template string should have this form: 

`?api-key=<API_KEY>&artist=%A&title=%t&album=%T&label=%L`

StationPlaylist will swap all of the parameters listed below for the corresponding track values.

The only additional consideration for this string is the `api-key` param. This inclusion is necessary to ensure we have access to credentials to complete an authenticated call to the backing NextUp API.

## Cloud Function

