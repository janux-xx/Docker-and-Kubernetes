# T03-01 Docker Compose

## Build the app

    docker compose build


## Run the app

    docker compose up -d

When the app will run, launch the voting app in your browser http://localhost:5000


## List the containers

    docker compose ps

## Look at the db container logs

    docker compose logs -f web-fe


## Compose V2 commands

LS will list the current projects

    docker compose ls

## Let's try to deploy a second version

    docker compose up -d

## Deploy a second version using a different project name

Let's now use a project name to see if we can deploy a second version

    docker compose -p test up -d

This fails because the localhost port 5000 is already assigned.

Change the ports value from (on dokcer-compose.yaml file)

    - "5000:5000"

to

    - "5001:5000"

## Deploy again

    docker compose -p test up -d

How many versions do we have running?

Launch the voting app in your browser http://localhost:5001

    docker compose ls

## Cleanup

    docker compose down
    docker compose ls
    docker compose -p test down
    docker compose ls