# docker-credential-ecr-login
Amazon ECR Docker Credential Helper as a Docker image

This is [Amazon ECR Docker Credential Helper](https://github.com/awslabs/amazon-ecr-credential-helper) from [AwsLabs](https://github.com/awslabs) packaged as a Docker image.

Just add this shell script into your PATH:

`docker-credential-ecr-login`:
```sh
#!/bin/sh
docker run -i --rm redbadger/docker-credential-ecr-login $1
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
