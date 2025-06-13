# L01-02 The Docker Containers

Type the following Docker commands:

## Pull and run a Nginx server

    docker run -d -p 8080:80 --name webserver nginx
 Output:
```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
56b81cfa547d: Pulling fs layer
dad67da3f26b: Pulling fs layer
32e44235e1d5: Pulling fs layer
3b00567da964: Pulling fs layer
d2a7ba8dbfee: Pulling fs layer
1bc5dc8b475d: Pulling fs layer
979e6233a40a: Pulling fs layer
Digest: sha256:6784fb0834aa7dbbe12e3d7471e69c290df3e6ba810dc38b34ae33d3c1c05f7d
Status: Downloaded newer image for nginx:latest
0f3078e9b2f30433c586bc4b7621e8f05fd2780b13fed73f8bb1695d1c721a9f
```

## List the running containers

    docker ps

Output:

```log
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                  NAMES
0f3078e9b2f3   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8080->80/tcp   webserver
```

## List the images

    docker images

## Attach to the container

    docker container exec -it  webserver bash  

Exit by typing

    exit

## Stop the container

    docker stop webserver

## Remove the container from memory

    docker rm webserver

## Remove the image

    docker rmi nginx