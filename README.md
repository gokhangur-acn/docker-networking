# How to set up?
- Guide : https://www.youtube.com/watch?v=9dljhdzRHD0&t=2s
- Repo : https://hub.docker.com/r/linuxserver/wireshark
- Copy docker-compose.yml from repo.
- Run docker-compose
```
docker-compose up
```

- wirehsark should be available on `http://localhost:3000/`


**note that**

> When using volumes (-v flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user PUID and group PGID.
Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.