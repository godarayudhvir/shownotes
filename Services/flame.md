# Flame - Dashboard

![](https://raw.githubusercontent.com/pawelmalak/flame/master/.github/home.png)

## Description

Flame is self-hosted startpage for your server. Its design is inspired (heavily) by [SUI](https://github.com/jeroenpardon/sui).
Flame is very easy to setup and use. With built-in editors, it allows you to setup your very own application hub in no time - no file editing necessary.

## Functionality

- 📝 Create, update, delete your applications and bookmarks directly from the app using built-in GUI editors
- 📌 Pin your favourite items to the homescreen for quick and easy access
- 🔍 Integrated search bar with local filtering, 11 web search providers and ability to add your own
- 🔑 Authentication system to protect your settings, apps and bookmarks
- 🔨 Dozens of options to customize Flame interface to your needs, including support for custom CSS, 15 built-in color themes and custom theme builder
- ☀️ Weather widget with current temperature, cloud coverage and animated weather status
- 🐳 Docker integration to automatically pick and add apps based on their labels

### Installation

Create a New flame directory and browse to it

```bash
mkdir -p /home/username/docker/flame
cd /home/username/docker/flame
```

Create a docker-compose file and paste contents from below

```bash
nano docker-compose.yml
```

```bash
version: '3.6'

services:
  flame:
    image: pawelmalak/flame
    container_name: flame
    volumes:
      - /home/username/flame/data:/app/data #change username with your username
      - /var/run/docker.sock:/var/run/docker.sock # optional but required for Docker integration
    ports:
      - 80:5005 #change 80 with port you want
    environment:
      - PASSWORD=password4flame
    restart: unless-stopped
```

Run the command below

```bash
docker compose up -d
```

Expected output

```bash
[+] Running 1/1
 ✔ Container flame  Started
```

Verify Docker Status (if it shows healthy and up 👍)

```bash
docker ps
```

Now access web GUI

- At http://127.0.0.1:80 or http://localhost:80

- Replace 80 with port number you provided

- Incase yours is 80 too, then you only need to type `127.0.0.1` in browser

![](https://i.imgur.com/dX6zAkn.png)

Enable Dark Theme and Login using the credential provided in compose file

![](https://i.imgur.com/jv1b7Bo.gif)

## General Settings

![](https://i.imgur.com/3xd134F.gif)

## Interface Settings

Set custom page title

![](https://i.imgur.com/vcLn7Qj.png)

## Weather Settings

Get api from https://www.weatherapi.com/

- Create account

- Free Plan is good enough

- Login and copy API Key

- Paste on FLAME's Weather > API Key Section

![](https://i.imgur.com/RR9PsG9.png)

![](https://i.imgur.com/4ut0Q1D.png)

- Click on Get current location

- and choose metrics and what additional data to show

![](https://i.imgur.com/wRwweHY.png)

## Docker Settings

In order to use the Docker integration, each container must have the following labels:

```yml
labels:
  - flame.type=application # "app" works too
  - flame.name=My container
  - flame.url=https://example.com
  - flame.icon=icon-name # optional, default is "docker"
# - flame.icon=custom to make changes in app. ie: custom icon upload
```

> "Use Docker API" option must be enabled for this to work. You can find it in Settings > Docker

You can also set up different apps in the same label adding `;` between each one.

```yml
labels:
  - flame.type=application
  - flame.name=First App;Second App
  - flame.url=https://example1.com;https://example2.com
  - flame.icon=icon-name1;icon-name2
```

### Adding the labels to existing images

Edit the docker compose file of the desired docker container
and add the labels like below for icon names refer to 
[Material Design Icons - Icon Library - Pictogrammers](https://pictogrammers.com/library/mdi/)

![](https://i.imgur.com/JA4UBe5.png)

Now rebuild that docker container with

```bash
docker compose up -d
```

Now let's enable Docker API on Flame

![](https://i.imgur.com/WvRQ1KU.gif)

### Custom CSS

![](https://i.imgur.com/GYlfmxy.gif) 

Get the above theme here: [Teraskull](https://gist.github.com/Teraskull/1e1c30923617b28f6fc0d331c1d854e9) 
Wanna Make your own ? Refer to this
[Custom CSS · pawelmalak/flame Wiki · GitHub](https://github.com/pawelmalak/flame/wiki/Custom-CSS)

And this is how mine looks (Emoji ain't included)

![](https://i.imgur.com/DMMmOKk.png)

### Adding Bookmark

![](https://i.imgur.com/hom8Eha.gif)

### Advanced Flame Customization

Contents of Docker container
![](https://i.imgur.com/eQLmu5F.png)
![](https://i.imgur.com/vT8wJMo.png)

Creat index.html file in flame/public

```yml
      - /home/cyberalliance/docker/flame/public/index.html:/app/public/index.html
```

Remove the container and rebuild it

Now edit the html file and paste the contents below

```html
<!doctype html>
<html lang="en">
    <head><meta charset="utf-8"/>
        <link rel="icon" href="/icons/favicon.ico"/>
        <link rel="apple-touch-icon" href="/icons/apple-touch-icon.png"/>
        <link rel="apple-touch-icon" sizes="57x57" href="/icons/apple-touch-icon-57x57.png"/>
        <link rel="apple-touch-icon" sizes="72x72" href="/icons/apple-touch-icon-72x72.png"/>
        <link rel="apple-touch-icon" sizes="76x76" href="/icons/apple-touch-icon-76x76.png"/>
        <link rel="apple-touch-icon" sizes="114x114" href="/icons/apple-touch-icon-114x114.png"/>
        <link rel="apple-touch-icon" sizes="120x120" href="/icons/apple-touch-icon-120x120.png"/>
        <link rel="apple-touch-icon" sizes="144x144" href="/icons/apple-touch-icon-144x144.png"/>
        <link rel="apple-touch-icon" sizes="152x152" href="/icons/apple-touch-icon-152x152.png"/>
        <link rel="apple-touch-icon" sizes="180x180" href="/icons/apple-touch-icon-180x180.png"/>
        <meta name="viewport" content="width=device-width,initial-scale=1"/>
        <meta name="description" content="Flame - self-hosted startpage for your server"/>
        <link rel="stylesheet" href="/flame.css"/><title>Flame</title><script defer="defer" src="/static/js/main.887e49c8.js">

        </script><link href="/static/css/main.289a6408.css" rel="stylesheet">
        </head>
        <body>
            <noscript>You need to enable JavaScript to run this app.</noscript>
            <div id="root"></div>
        </body>
        </html>
```

We now have a editable index.html file yeah!!

Now edit the .html file as per your requirements and CSS from the previously showcased settings

I added a chatbot here
![](https://i.imgur.com/pxakc72.png)

And also changed the favicon 👍

Well that's how you create a dashboard with Flame.

## Access from outside the network

These are few ways how we can go about doing that

1. If you have a domain name such as example.com
   then you might wanna setup a reverse proxy using
   
   - Nginx Proxy Manager
   
   - [Cloudflare Tunnel](https://github.com/godarayudhvir/shownotes/blob/main/Cloudflare/cf_tunnel.md)
   
   - Traefik
   
   - & More

2. If you don't have a domain name or don't want public accessing it
   setup VPN one of the following services
   
   - Tailscale
   
   - Twingate
   
   - & More
