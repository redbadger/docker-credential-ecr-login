# docker-credential-ecr-login
Amazon ECR Docker Credential Helper as a Docker image

This is [Amazon ECR Docker Credential Helper](https://github.com/awslabs/amazon-ecr-credential-helper) from [AwsLabs](https://github.com/awslabs) packaged as a Docker image.

Just add an executable shell script called `docker-credential-ecr-login` into your PATH:

1. If you are using EC2 instance profile:

    ```sh
    #!/bin/sh
    docker run \
      -i \
      --rm \
      -v /etc/ssl/certs:/etc/ssl/certs \
      redbadger/docker-credential-ecr-login $1
    ```

1. If you are using environment variables:

    ```sh
    #!/bin/sh
    docker run \
      -i \
      --rm \
      -e AWS_ACCESS_KEY_ID \
      -e AWS_SECRET_ACCESS_KEY \
      -e AWS_SESSION_TOKEN \
      -v /etc/ssl/certs:/etc/ssl/certs \
      redbadger/docker-credential-ecr-login $1
    ```

1. If you are AWS credentials:

    ```sh
    #!/bin/sh
    docker run \
      -i \
      --rm \
      -v /etc/ssl/certs:/etc/ssl/certs \
      -v $HOME/.aws/credentials:/root/.aws/credentials \
      redbadger/docker-credential-ecr-login $1
    ```

Then modify `~/.docker/config.json` to let Docker know to use the helper (substituting your AWS account and region):

```json
{
  "credHelpers": {
    "${account}.dkr.ecr.${region}.amazonaws.com": "ecr-login"
  }
}
```

or (for all registries)...

```json
{
  "credsStore": "ecr-login"
}
```
