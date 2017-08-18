# Build the image from the Dockerfile 

    docker build -f docker-gotty-master/Dockerfile -t gotty .

# Run GoTTY commands inside a Docker container

    docker run -p 9077:8080 -it gotty -w /bin/bash


*Open a browser at http://localhost:9077*
