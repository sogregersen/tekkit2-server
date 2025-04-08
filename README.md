
# Tekkit 2 Server

This Docker image provides a ready-to-use Tekkit 2 server, a renowned modpack for Minecraft that blends technology and adventure. The image is built upon "mcr.microsoft.com/openjdk/jdk:8-mariner" and includes all necessary dependencies to run a Tekkit 2 server seamlessly.

https://hub.docker.com/repository/docker/gregdock97/tekkit2-server/gene

## IMAGES

| TAG        | Tekkit version |
| ---------- | -------------- |
| latest     | 1.2.5          |
| alpine     | 1.2.5          |
| rpi4       | 1.2.5          |
| 1.2.4      | 1.2.4          |

## OBS,OBS

Base-image change from *ALPINE* to *CBL-MARINER*, for those who still want to use *ALPINE* need to change the tag to "alpine"


**Features:**

- Automated setup and configuration of the Tekkit 2 server.
- Exposes the default Minecraft port 25565. 

**Usage:**

To deploy the server using Docker Compose, create a `docker-compose.yml` file with the following content:

```yaml
version: '3.8'

services:
  tekkit2-server:
    image: gregdock97/tekkit2-server:latest # Add :rpi4 for the raspberry image
    container_name: tekkit2-server
    restart: unless-stopped
    ports:
      - "25565:25565"
    environment:
      MEMORY: 15G      # Adjust RAM here!
      TZ: Europe/Oslo  # Remember change!
    volumes:
      - tekkit2-data:/tekkit2

volumes:
  tekkit2-data:
```

**Instructions:**

1. **Start the Server:**

   In the directory containing the `docker-compose.yml` file, run:

   ```bash
   docker-compose up -d
   ```

   This command will download the image and start the Tekkit 2 server in detached mode.

2. **Accessing Server Files:**

   The server's data is stored in a Docker volume named `tekkit2-data`. To access or back up your world data and configurations, you can inspect this volume.



# CLI

Or just rum this in the commandline:

```bash
docker run -d --name tekkit2-server \
  -p 25565:25565 \
  -v tekkit2-data:/tekkit2 \
  -e MEMORY=5G \
  -e TZ=Europe/Oslo \
  --restart unless-stopped \
  gregdock97/tekkit2-server:latest
```

# Raspberry Pi

Just change the image to:

```yaml 
gregdock97/tekkit2-server:rpi4 
```

