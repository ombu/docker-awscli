Lightweight Docker image with the AWS and ECS CLI tools
======================================================

Build the Docker image
----------------------

    docker build -t ombu/awscli:latest .

Run
---

To run AWS commands, export your AWS credentais to the environment:

    export AWS_DEFAULT_REGION=us-west-2
    export AWS_ACCESS_KEY_ID=...
    export AWS_SECRET_ACCESS_KEY=...

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/awscli aws --help

    docker run \
        -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/awscli ecs-cli --help

