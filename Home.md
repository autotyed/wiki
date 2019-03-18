#### This wiki is still under development! - March 20, 2019

[Autotyde](https://github.com/davidnewhall/autotyed) is a collection of scripts,
web site (html, javascript, css, images), launchagents (for macos), systemd service
units (for linux), and installation instructions. The components provided in this
repo allow you to quickly setup and configure a full-blown media, home automation
hub and security server on a Mac. If you're using Linux, then these components are
limited to media, but could include other options in the future.

I run all of the following software on a single Mac server.

#### My Mac Server

- Contains 64TB of storage for media (Movies, TV, Music) using [LSI Raid card](https://www.amazon.com/LSI-Logic-SAS9260-8I-8PORT-512MB/dp/B002IT4YG2).
- Has a custom web interface (this repo!) using valid SSL, and available from the Internet.
  - The web interface allows full access to the apps below (those that provide their own web interface).
- Controls over 200 home automation switches and sensors
- Detects motion on, and records video from 8 IP security cameras
- Controls [2 switches](https://store.ui.com/collections/routing-switching/unifi), [3 WAPs](https://www.ui.com/unifi/unifi-ap-ac-pro/) and a [router](https://www.ui.com/unifi-routing/unifi-security-gateway-pro-4/).
- Graphs everything. Server metrics, house lights, temps, doors, windows, energy; *.
- Runs the following software:
  - [Deluge](https://deluge-torrent.org) - Manages media downloaded through torrents.
  - [SecuritySpy](https://www.bensoftware.com/securityspy/) - Detects motion on IP cameras; provides triggers to home automation.
  - [Indigo](https://www.indigodomo.com) - Customizable and programmable home automation solution
  - [Sonarr](https://sonarr.tv) - TV Series Library
  - [Radarr](https://radarr.video) - Movie Library
  - [Lidarr](https://lidarr.audio) - Music Library
  - [Bazarr](https://github.com/morpheus65535/bazarr) - Retrieves subtitles for all movies and tv shows
  - [Jackett](https://github.com/Jackett/Jackett) - Allows Sonarr and Radarr to use custom trackers.
  - [NZBGet](https://nzbget.net) - This downloads media from newsgroups.
  - [Plex](https://www.plex.tv) - This allows my family and friends to watch all my media.
  - [Tautulli](https://tautulli.com) - Provides insights and graphs into details Plex usage
  - [Ubiquiti UniFI Controller](https://www.ui.com/download/unifi) - Controls the network gear.
  - [Grafana](https://grafana.com) - Contains graphs for EVERYTHING.
  - [Nginx](https://www.nginx.com) - Web server with auto-renewing SSL cert from [Let's Encrypt](https://letsencrypt.org) using [certbot](https://certbot.eff.org)
  - [InfluxDB](https://www.influxdata.com) - Time series database for Grafana backend
  - [Telegraf](https://www.influxdata.com/time-series-platform/telegraf) - Collects network metrics and custom metrics for Sonarr, Radarr & Plex.
  - [Glances](https://nicolargo.github.io/glances/) - stores systems metrics in InfluxDB
  - [unpacker-poller](https://github.com/davidnewhall/unpacker-poller) - to extract Deluge downloads
  - [unifi-poller](https://github.com/davidnewhall/unifi-poller) - optionally store UniFI controller metrics in InfluxDB

#### Autotyde Purpose

I'm trying to show you how to achieve what I did. Not just show you, but provide
directions, scripts and startup daemons to make it all work. I'm also giving you
the custom web interface (it's pretty simple, but elegant and powerful), and the
nginx routes to make all these desperate apps work on a single domain. Plex,
specifically, has some very custom rules to make it work via SSL only and through
nginx. You can run most of this stack on Linux, but if you do with a Mac (or a
powerful hackintosh), you can even get full access to SecuritySpy and Indigo
(including Indigo Touch) through the same https URL.

Not only does my media system keep itself completely updated and provide a cool
web interface, it has graphs! My network is completely graphed (switches,
clients, router, access points - you name it) using unifi-poller. I created
custom telegraf scripts to dump data into InfluxDB about the media libraries, so
that data is all graphed too. Glances and telegraf both create system-level
metrics; things like load, disk usage, memory utilization, context switching and
so on.

There are so many custom pieces here, especially when you start digging into my
Indigo configuration, but I will attempt to document everything I can. I'm writing
this for myself, really. I'm giving it to you, but this is my baby and I want to
be able to recreate it if the water heater next to it ever explodes.
