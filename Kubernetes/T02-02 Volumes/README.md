# L02-01   Volumes

## Open a terminal and create a volume

    docker volume create myvolume

## List the volumes

    docker volume ls

## Run a Nginx container that will use the volume

    docker run -d --name volumetest -v myvolume:/app nginx:latest

    docker ps

    docker ps -a

## Connect to the instance

    docker exec -it volumetest bash

## Let’s create a file in the volume using Nano

    apt-get update
    apt-get install nano -y

## Create a file in the app folder
    cd app
    nano test.txt

Type something, save the file and exit Nano using:

    CTRL-O
    - Hit ENTER
    CTRL-X

Detach from the instance:

    exit

## Stop and remove the container

    docker stop volumetest
    docker rm volumetest

## Run it again and see if the file still exists

    docker run -d --name volumetest -v myvolume:/app nginx:latest
    docker exec -it volumetest bash
    cd app
    cat test.txt

## Cleanup

    docker volume rm myvolume
    docker stop volumetest
    docker rm volumetest

## Used volumes can't be deleted

   ```
   docker volume rm myvolume
   ```