FROM nginxdemos/hello
COPY nginx.conf /etc/nginx/
EXPOSE 1792
CMD ["nginx", "-g", "daemon off;"]


#docker build -t ngnix_gg .
#docker run --rm --network bridge_gg -d -p 1792:1792 --rm --name t2 --ip 172.17.0.3 ngnix_gg
#docker run --rm --network bridge -d -p 1792:1792 --rm --name t2 ngnix_gg