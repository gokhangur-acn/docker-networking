# How to set up?
- Guide : https://www.youtube.com/watch?v=9dljhdzRHD0&t=2s
- Repo : https://github.com/linuxserver/docker-wireshark, https://hub.docker.com/r/linuxserver/wireshark
- Copy docker-compose.yml from repo.
- Run docker-compose
```
docker-compose up
```
- wireshark should be available on `http://localhost:3000/`


**note that**

> The `host` networking driver only works on Linux hosts, and is not supported on Docker Desktop for Mac, Docker Desktop for Windows, or Docker EE for Windows Server. (https://docs.docker.com/network/host/)


> When using volumes (-v flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user PUID and group PGID.
Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.


```
docker run --name=wireshark --rm --net=host --cap-add=NET_ADMIN -e PUID=0 -e GUID=0 -e TZ=Europe/London -p 3000:3000  -v ./data:/config lscr.io/linuxserver/wireshark:latest
```
