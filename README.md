Lightweight Docker image with an assortment of AWS CLI tools
============================================================

This image includes:

- AWS CLI, via Amazon Linux 2 yum package
- Session Manager plugin, via <https://s3.amazonaws.com/session-manager-downloads/plugin/latest/linux_64bit/session-manager-plugin.rpm>
- ECS CLI, via <https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest>
- awslogs, via <https://pypi.org/project/awslogs/>
- cfn-lint, via <https://pypi.org/project/cfn-lint/>

Build the Docker image
----------------------

    docker build -t ombu/docker-awscli:latest -f Dockerfile .


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
    export AWS_SECRET_ACCESS_KEY=...d

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

SSM session:

    docker run \
        -it -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
        ombu/docker-awscli ssm start-session --target <instance-id>

Helpful shell aliases
---------------------

    alias aws="docker run --rm --name awscli -v ${PWD}:/tmp -w /tmp -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION ombu/docker-awscli aws"

    alias ssm-session="docker run -it --rm -v ${PWD}:/tmp -w /tmp -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION ombu/docker-awscli aws ssm start-session --target"

    alias cf-lint="docker run --rm -v $PWD:/tmp ombu/docker-awscli cfn-lint"

    alias awslogs="docker run --rm -v $PWD:/tmp ombu/docker-awscli awslogs"

    alias ecs-cli="docker run --rm -v $PWD:/tmp ombu/docker-awscli ecs-cli"

