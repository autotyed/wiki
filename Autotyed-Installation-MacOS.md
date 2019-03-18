This page contains a walkthrough of the Autotyde Installation and a link to a
youtube video with a video guide.

## Basic Instructions

This is from memory, just a start, and is under refinement.

### Install Plex Server
- [Install the Plex Server](https://support.plex.tv/articles/200288586-installation/). Configure it to auto-start. Link it to your account, etc.
- XXX: Add more details after installing plex.

### Install Open Source Software
Install all of the open source applications using the scripts in this repo.
`make install` is a great shortcut to run them all automatically.
Recommend reading through the scripts in the
[scripts/macos](../../tree/master/scripts/macos) folder.
Escpecially those that mess with apps you already have installed.
- `make install` installs:
  - `Radarr`, `Lidarr`, `Sonarr`, `Bazarr`, `Tautulli`, `Deluge`, `NZBGet`, `Jackett`
  - `Homebrew`, `Nginx`, `InfluxDB`, `Grafana`, `Glances`, `Telegraf`, `certbot`
  - It also does basic configuration for a few of these apps.

## Post Installation
After installing all the lovely software there are a few things you need to do.
The following are quick directions. Use the navigation links to the right to find
detailed information for each of these applications. (soon, still working on those)

### Configure Open Source Software
Some of the apps you just installed are going to require you to open their
web interface and provide additional configuration details. Follow along!

##### Nginx
After installation, Nginx is in a reaosnable state, but there are a few more
things you can do to make it better. It's using a self-sign certificate, but
you can get one for free if your site is reachable from the Internet, so do that.

###### Setup certbot for SSL
XXX: ...figure this out and document it.

###### Update nginx.conf
There is a snippet of configuration at the
[root of the repo](../../tree/master/nginx.conf). You should put the portion in
the `http {}` block into `/usr/local/etc/nginx.conf` in the `http {}` block.

##### Configure Tautulli
- Tautulli needs to have the wizard completed before it's fully configured.
- It should pop up automatically. If not, go to it directly at this link:
  - http://localhost:8181/welcome

##### Configure Bazarr
- Be sure to set the correct Base URL when you navigate to the [Bazarr page](https://localhost/bazarr/wizard) for the first time.
- You should just do that now. Go here: https://localhost/bazarr/wizard
  - The Base URL is `/bazarr/` (both slashes required).
- For path mappings, enter one value each for Sonarr and Radarr: `/ -> /` (slashes on both sides)
- Choose your preferred language(s) and Select `Default Enabled` for Series and Movies.
- You'll also need to configure Bazarr's access to Sonarr and Radarr.
- Fetch the API Keys for each app by navigating to their respective configuration interfaces:
  - [Sonarr](https://localhost/sonarr/settings/general) (Base URL: `/sonarr`) - [Radarr](https://localhost/radarr/settings/general) (Base URL: `/radarr`)
- If Bazarr gets stuck restarting, use these commands to kick it:
  - `launchctl unload ~/Library/LaunchAgents/com.github.morpheus65535.bazarr.plist`
  - `launchctl load ~/Library/LaunchAgents/com.github.morpheus65535.bazarr.plist`

##### Configure Jackett.
Add your trackers. Use google if you need help with this because it's pretty much specific to you.
Will try to add more information here as it becomes available.

##### Configure Deluge
- You have to [connect to the interface](https://localhost/deluge) first, log in with the default password `deluge`, and connect the web interface to the backend service.
- Enable the label plugin and add labels: `lidarr`, `tv-sonarr`, `radarr`
  - Use these same names to keep things simple and identical to my configuration.

##### Configure NZBGet
If you have news group access, navigate to the [NZBGet interface](https://localhost/nzbget) and configure the application with your server details. Lots of information on the Internet about how to do that. Google it. Configure NZBGet to start on login; this
is a setting in the application.

##### Configure Sonarr, Radarr and Lidarr.
You have to add your trackers (Jackett API, and/or direct sites) and download
clients to all of Sonarr, Radarr and Lidarr. This document will not cover that
process too much since it's widely available elsewhere.

##### Configure Grafana
Oh, Grafana. After running the install script Grafana should be up and running
and accessible from your web interface. It does not have any dashboards, at least
not until I find a nifty way to script their automatic installation. Hopefully
the dashboards get uploaded to the repo soon. Install those into Grafana and tune
them for your environment. The disk graphs, for instance, are very specific to my
server; fix them for yours.

## Optional Components

#### Install and Configure SecuritySpy
If you have security cameras and a mac server you should have SecuritySpy.
Go check it out. It's not terribly expensive and the features make it well worth
the minuscule cost. The developer offers discounted upgrades as well, he's
extremely responsive when requesting support and he listens to his users.
XXX: ...more

#### Install and Configure Indigo
Download and install Indigo from their website. This application is commercial
and requires a yearly license. If you're into home automation and you know Python
this application is for you. You can literally tie it into everything with a very
intuitive interface. It has an ability to create custom web pages used to control
various aspects of your home.

Indigo has some interesting security considerations in the context of autotyed.
XXX: ...insert more here.

#### Install and Configure UniFi Controller
A cloud key works too. If you're using the UniFI controller there is not much
special configuration needed specific to autotyed. Just leave the app on port 8443.
If you're using a CloudKey edit the provided nginx config to have the correct IP
in the proxy_pass directive.
