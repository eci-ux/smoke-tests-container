# Smoke Tests Container

Docker image for running the smoke tests with Puppeteer

## How to build the image
```
export VERSION=v1 # can be a git tag

docker build \
  -t docker.pkg.github.com/eci-ux/smoke-tests-container/smoke-tests-container:$VERSION .
```
Every push on master will create a new image version with the latest tag automatically.

## How to use

### With docker
```
docker run \
  -it \
  --rm \
  -v $PWD/my-smoke-tests:/tests \
  -w /tests \
  docker.pkg.github.com/eci-ux/smoke-tests-container/smoke-tests-container:$VERSION
```

### With docker-compose
Add this section to your `docker-compose.yml` file, if you want to wait for another container or host to be ready before running the tests, add the environment section with the host and port, this will make the `npm start` command to wait.
```
smoke-tests:
  image: docker.pkg.github.com/eci-ux/smoke-tests-container/smoke-tests-container:latest
  volumes:
    - ./my-smoke-tests:/tests
  environment:
    WAIT_HOSTS: my-app:8080
```
