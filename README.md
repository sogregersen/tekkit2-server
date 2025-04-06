# Tekkit 2 Server

This Docker image provides a ready-to-use Tekkit 2 server, a renowned modpack for Minecraft that blends technology and adventure. The image is built upon "openjdk:8-jdk-alpine" and includes all necessary dependencies to run a Tekkit 2 server seamlessly.

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
      TZ: Eurpoe/Oslo  # Remember change!
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





# CHANGES
**2025-04-04**
- Added Raspberry Pi Image on :rpi4 tag
- rpi4 image is based on "mcr.microsoft.com/openjdk/jdk:8-mariner"

**2025-04-03**
- UPDATED to TEKKIT 2 - 1.2.5
- Made a Launch.sh file that runs the CMD command form earlier versions
- Removed :old tag
- added TZ veriable

**2025-02-15**
- Added the option to change the RAM, default value is 5GB
- Deleted some obeselete files
- added a new image "old", for the first image with no RAM change (20 GB)
