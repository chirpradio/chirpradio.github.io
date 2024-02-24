---
layout: page
title: NextUp
permalink: /nextup/
nav_order: 1
parent: Active Projects
---

# NextUp
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
* [Github Repo](https://github.com/chirpradio/nextup)
* Slack Channel: [#proj-nextup](https://chirpdev.slack.com/archives/C01GW3BRV5H)
* [Dev Instance](https://nextup-dot-chirpradiodev.appspot.com/login?redirect=%2Flibrary)
* [Production Instance](https://nextup.chirpradio.org/)
* [API Documentation](https://nextup-dot-chirpradiodev.appspot.com/api)

## What is NextUp?
NextUp is the successor to the [Legacy DJ Database app](legacy_dj_app.md). When it launches, it will be used by all CHIRP DJs and Music Department staff to perform essential tasks related to our music metadata library, including vital on-air tasks.

Current Functionality Includes:
* CRUD, search, and tagging/sorting functionality for album metadata in the music database
* Save albums to personalized crates
* Push song metadata to the on-air playlist
* View DJ Traffic Log (the schedule of promos and station information that must be read on-air by the DJs)

## Tech Specs
NextUp is written in Vue.js/Javascript, and uses Elasticsearch. The app is hosted on Google Cloud.
A recording from our 2024 meeting "NextUp Demo and Q&A" can be found in Slack [here](https://chirpdev.slack.com/archives/C01GSPCEDMK/p1706757506383289).

# How To Contribute
* Instructions for setting up for local development can be found [here](https://github.com/chirpradio/nextup/blob/develop/setup.md).
* Check out the backlog in [Trello](https://trello.com/b/B1L4W9A9/dev-projects) for a list of unassigned tasks tagged "NextUp" that are waiting to be worked on.

# Developer Documentation

## Playlist pipeline [WIP]
NextUp uses a set of microservices that run as [Cloud Functions](https://cloud.google.com/functions/#documentation) and communicate through [Cloud Pub/Sub](https://cloud.google.com/pubsub/#documentation) messages to enrich freeform tracks with images and let the website and mobile apps know what's playing.

```mermaid
flowchart TB
    NextUp[fa:fa-record-vinyl NextUp] 
    NextUp --> |Pub/Sub<br>playlist-event| process(fa:fa-code processPlaylistTrack)    
    subgraph storage
        update(fa:fa-code updatePlaylistStorage)
        cloud(fa:fa-bucket playlist.json)
        update --> |builds & saves| cloud
    end
    process --> |Pub/Sub: playlist-track-processed | storage    
    storage -->|Pub/Sub: playlist-storage-updated| notify(fa:fa-code notifyLiveSite)
    notify --> |GET| website(fa:fa-globe chirpradio.org)
    website --> |GET| cloud
```

### Topic: "playlist-event"
{: .no_toc }
The NextUp API added a track to the playlist, updated a track on the playlist, or deleted a track from the playlist

#### Message data
{: .no_toc }

| Field Name   | Type            | Description |
|:-------------|:----------------|:------------|
| action       | String          | "added", "updated", or "deleted"  |
| track        | [PlaylistEvent](https://github.com/chirpradio/nextup/blob/develop/app/models/playlistevent.model.js)   | The plain JSON output of the PlaylistEvent entity from the Datastore. Keys *have not* yet been replaced with the related entities they reference (e.g., the `artist` value is a key). |

#### Subscriber(s)
{: .no_toc }

- processPlaylistTrack
  - checks LastFM for images it can add to the PlaylistEvent entity
  - retrieves the details of related objects from the NextUp database for the benefit of later steps in the pipeline
    - album
    - artist
    - track
    - selector (i.e., the DJ)
  - publishes a message to the "playlist-track-processed" topic

### Topic: "playlist-track-processed"
{: .no_toc }

The track data has been enriched and can be used by later steps without querying the Datastore

#### Message data
{: .no_toc }

| Field Name   | Type            | Description |
|:-------------|:----------------|:------------|
| action       | String          | "added", "updated", or "deleted"  |
| track        | [PlaylistEvent](https://github.com/chirpradio/nextup/blob/develop/app/models/playlistevent.model.js)   | The plain JSON output of the PlaylistEvent entity from the Datastore. If the track is added or updated, keys *have* been replaced with the entities they reference (e.g., the `artist` value is an object with details on the artist).  |

#### Subscriber(s)
{: .no_toc }

- updatePlaylistStorage 
  - builds and saves the public JSON feed of recently played tracks to a Cloud Storage bucket
  - publishes a message to the "playlist-storage-updated" topic

### Topic: "playlist-storage-updated"
{: .no_toc }

The JSON feed that lists the track playing now and the five most recently played tracks before it has been updated.

#### Message data
{: .no_toc }

_a passthrough of the "playlist-track-processed" message_

| Field Name   | Type            | Description |
|:-------------|:----------------|:------------|
| action       | String          | "added", "updated", or "deleted"  |
| track        | [PlaylistEvent](https://github.com/chirpradio/nextup/blob/develop/app/models/playlistevent.model.js)   | The plain JSON output of the PlaylistEvent entity from the Datastore. If the track is added or updated, keys *have* been replaced with the entities they reference (e.g., the `artist` value is an object with details on the artist).  |

#### Subscriber(s)
{: .no_toc }
- notifyLiveSite: calls endpoints at chirpradio.org that prompt it to retrieve the latest version of playlist.json from the Cloud Storage bucket
