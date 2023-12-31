# What are we hosting today ?

A fancy self-hosted monitoring tool called [uptime-kuma](https://github.com/louislam/uptime-kuma)

### ![](https://user-images.githubusercontent.com/1336778/212262296-e6205815-ad62-488c-83ec-a5b0d0689f7c.jpg)

### Live Demo 🤹‍♀️

Tokyo Demo Server: [https://demo.uptime.kuma.pet](https://demo.uptime.kuma.pet/) 
(Sponsored by [Uptime Kuma Sponsors](https://github.com/louislam/uptime-kuma#%EF%B8%8F-sponsors))

It is a temporary live demo, all data will be deleted after 10 minutes. Use the one that is closer to you, but I suggest that you should install and try it out for the best demo experience.

### ⭐ Features

- Monitoring uptime for HTTP(s) / TCP / HTTP(s) Keyword / HTTP(s) Json Query / Ping / DNS Record / Push / Steam Game Server / Docker Containers
- Fancy, Reactive, Fast UI/UX
- Notifications via Telegram, Discord, Gotify, Slack, Pushover, Email (SMTP), and [90+ notification services, click here for the full list](https://github.com/louislam/uptime-kuma/tree/master/src/components/notifications)
- 20-second intervals
- [Multi Languages](https://github.com/louislam/uptime-kuma/tree/master/src/lang)
- Multiple status pages
- Map status pages to specific domains
- Ping chart
- Certificate info
- Proxy support
- 2FA support

### Who's the author ?

https://github.com/louislam

### What do we need ?

1. Some Kind of Ubuntu Environment
   
   - WSL Running Ubuntu
   
   - Ubuntu on a machine
   
   - Ubunut on a VM

2. Docker and Docker-compose Installed

### Skill Prerequisite ?

- Basic Ubuntu

- Basic Docker

## How to Install 🔧

Firstly Create a folder named Docker inside home/username Directory
Inside that create a folder named uptime-kuma

1. **Create a Directory Structure**:
   
   - Start by creating a directory named `Docker` inside your home directory. This will serve as the root directory for your Docker-related files and projects.
   
   - Open your terminal or command prompt and navigate to your home directory using the `cd /home/username` 
   
   - Create the `Docker` directory:
     
     ```bash
     mkdir Docker
     ```

2. **Create a Specific Project Folder**:
   
   - Inside the `Docker` directory, create a subfolder named `uptime-kuma`. This subfolder will be dedicated to storing our docker compose file and other config if required.
   
   - Navigate into the `Docker` directory:
     
     ```bash
     cd Docker
     ```
   
   - Create the `uptime-kuma` folder:
     
     ```bash
     mkdir uptime-kuma
     ```

3. **Creating a Docker Compose file**:
   
   - Now create a docker compose file by using the command
     `nano docker-compose.yml` after navigating into uptime-kuma directory
   - Copy and paste the commands from below

```yaml
version: '3.8'

services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - /home/username/docker/uptime-kuma/data:/app/data
    ports:
      - "2000:3001"  # <Host Port>:<Container Port>
    restart: always

volumes:
  uptime-kuma:
```

### Docker-compose configuration break-down

1. **Compose File Version**:
   
   - The `version: '3.8'` line specifies the version of the Docker Compose file format being used. In this case, it’s version 3.8.
   - The version determines which features and syntax are available in the Compose file.

2. **Services**:
   
   - The `services` section defines the individual services (containers) that make up your application.
   - In your case, there’s one service named `uptime-kuma`.

3. **Service Configuration (uptime-kuma)**:
   
   - `uptime-kuma` service configuration:
     - **Image**: Specifies the Docker image to use for this service. In your case, it’s `louislam/uptime-kuma:1`.
     - **Container Name**: Sets the name of the container to `uptime-kuma`.
     - **Volumes**:
       - The `- /home/username/docker/uptime-kuma/data:/app/data` line creates a **bind mount**.
       - It maps the local directory `/home/username/docker/uptime-kuma/data` on your host to the `/app/data` directory inside the container.
       - This allows data to be shared between your host and the container.
     - **Ports**:
       - The `- "2000:3001"` line maps port 2000 on your host to port 3001 inside the container.
       - You can access the Uptime Kuma web interface on your host at `http://localhost:2000`.
     - **Restart Policy**:
       - The `restart: always` line ensures that the container restarts automatically if it stops unexpectedly.

4. **Volumes**:
   
   - The `volumes` section defines named volumes.
   - In your case, there’s a named volume named `uptime-kuma`.
   - Named volumes are useful for persisting data across container restarts.

In summary, your Docker Compose configuration sets up a single service (`uptime-kuma`) based on the specified image. It binds a local directory to the container, maps ports, and ensures the container restarts automatically. The named volume `uptime-kuma` allows data persistence.

### Spinning up 🐳 container

Run the command `docker compose up -d`

When you execute this command, Docker Compose reads your configuration file, creates and starts the specified services (containers), and detaches them in the background. It’s like bringing your multi-container application to life with a single command!

![](https://i.imgur.com/kQn9txn.png)

Check if the container is up & Running using the cmd `docker ps -a`

![](https://i.imgur.com/awptPgn.png)

If it's running then process to next section
else contact us if you need any help.

## Configuring the Instance ⚙

Browse to `127.0.0.1:2000` or `localhost:2000`
(change 2000 to the host port you had chosen in your Docker Compose configuration) to access the Uptime Kuma web interface.

![](https://i.imgur.com/vcoMf4Q.png)

Create your admin account

![](https://i.imgur.com/XnADpMU.png)

Now we've uptime-kuma running so lets configure it for use now

### Adding new monitors

1. Website (http) Monitoring
   
   - Click on add new monitor
   
   - Select Monitor Type HTTP(s)
   
   - Type in a Friendly Name | eg: Landing page
   
   - Type in the URL | eg: cyberalliance.in
   
   - Set heartbeat interval to your liking | eg: If you want uptime-kuma to check website status every 60 seconds then set it to 60
   
   - Set Retries - Maximum retries before the service is marked as down and a notification is sent
   
   - For the retry to you can set interval time
   
   - Under Advanced Settings
     
     - Enable Certificate Expiry Notification
     
     - Add to a monitor group | eg: Cyber Alliance India
     
     - Add a Description | eg: Land page of Cyber Alliance India
   
   - Add Tags, if any
   
   - Setup notification (**We'll come back to this later**)

> Proxy, HTTP, Ignore TLS/SSL, Accepted status code options and Upside down mode are Not covered in this guide atleast currently.

   ![](https://i.imgur.com/3FwrxPd.png)

### More configurations soon...

## Setting up for Remote Access 📡

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

## Updating Instance

## Backuping up & restoring Containers and Their volumes

https://wiki.opensourceisawesome.com/books/updating-docker-containers/page/update-docker-keep-your-data-too

## Going Plus Ultra 💪🏼

![](https://i.imgur.com/a3K5pTl.png)

![](https://i.imgur.com/hKNcNHe.png)

![](https://i.imgur.com/zs0KnmR.png)

docker create --name temp_container louislam/uptime-kuma:1
docker cp temp_container:/path/in/container /home/username/docker/uptime-kuma/
docker rm temp_container
