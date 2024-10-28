# UNC OSCAR Lab Docker Images

This is a repository for docker images for various projects in the
OSCAR lab.  Docker hub pulls from this repository to automatically
build and tag images in the oscar1ab namespace.

In general, images in this repository should be in a folder by project
name,a nd follow the instructions below.

# Building from scratch

For instance, to build the NeedleDB image, you would cd to the needledb directory.

`docker buildx build .`

For more detailed output, use:

`docker buildx build . --progress=plain`

You can confirm the built image is for multiple architectures using

`docker image inspect TAG`

where "TAG" is the name of the image.

The full command to build and push (requires privilege) is:

`docker buildx build --tag index.docker.io/oscar1ab/needledb:latest --platform linux/amd64 --push .`

## Push to dockerhub

Dockerhub is configured to automatically build and update the
`needledb:latest` tag upon a push to the master branch.

This can be configured for other image tags in the docker hub page.

Dockerhub also automatically builds images in response to a PR,
which should prevent merging changes that break the build.
