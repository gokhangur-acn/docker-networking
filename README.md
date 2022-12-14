# How to set up?
- Guide : https://www.youtube.com/watch?v=9dljhdzRHD0&t=2s
- Repo : https://github.com/linuxserver/docker-wireshark, https://hub.docker.com/r/linuxserver/wireshark
- Copy docker-compose.yml from repo.
- Run docker-compose
```
docker-compose up
```
- wireshark should be available on `http://localhost:3000/`


## Simple Networking Test
Reference: http://cloudyuga.guru/hands_on_lab/tcpdump_docker

1. Create a small container with tcpdump installed
```
docker build -t tcpdump_gg - <<EOF 
FROM ubuntu
RUN apt-get update && apt-get install -y tcpdump
CMD tcpdump -i eth0 -n
EOF
```

Or create a dockerfile with above commands to create the container. 

2. Create a new network
```
docker network create bridge_gg
```

3. Run a small container (ngnix) on the new network
```
docker run --rm --network bridge_gg -d -p 81:80 --rm --name t1 nginxdemos/hello
```

4. Inspect network setting for ngnix container
```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' t1
```


4. Run tcpdump container
```
docker run -it --rm --net=container:t1 tcpdump_gg
```

If you want to monitor a specific port.
```
docker run -it --rm --net=container:t1 tcpdump_gg tcpdump port 80 -A -n
```


**note that**

> The `host` networking driver only works on Linux hosts, and is not supported on Docker Desktop for Mac, Docker Desktop for Windows, or Docker EE for Windows Server. (https://docs.docker.com/network/host/)


> When using volumes (-v flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user PUID and group PGID.
Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.


```
docker run --name=wireshark --rm --net=host --cap-add=NET_ADMIN -e PUID=0 -e GUID=0 -e TZ=Europe/London -p 3000:3000  -v ./data:/config lscr.io/linuxserver/wireshark:latest
```
