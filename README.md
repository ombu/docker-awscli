Lightweight Docker image for AWS CLI tools
==========================================

This image contains the AWS CLI, ECS CLI, awslogs and cfn-lint

Build the Docker image
----------------------

    docker build -t ombu/docker-awscli:latest .


Push the image to Docker Hub
-------------------------------

The Github repository for this project is configured to trigger an automatic
build of a Docker image in https://hub.docker.com/r/ombu/docker-awscli/.

To trigger the build, push a commit on the master branch:

    git push

and watch the build progress at https://hub.docker.com/r/ombu/docker-awscli/builds/


Usage
-----

To run AWS commands, export your AWS credentials to the environment:

    export AWS_DEFAULT_REGION=us-west-2
    export AWS_ACCESS_KEY_ID=...
    export AWS_SECRET_ACCESS_KEY=...

AWS CLI:

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/docker-awscli aws --help

ECS CLI:

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/docker-awscli  ecs-cli --help

awslogs:

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/docker-awscli  awslogs --help

cfn-lint:

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/docker-awscli  cfn-lint --help
