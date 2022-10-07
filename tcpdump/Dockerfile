FROM ubuntu
RUN apt-get update && apt-get install -y tcpdump
CMD tcpdump -i eth0 -n

#docker build -t tcpdump_gg .