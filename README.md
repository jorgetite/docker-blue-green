# Docker App Faux
Docker App Faux creates a docker image based on [nginx:latest](https://hub.docker.com/_/nginx) that mocks a simple web app. The Dockerfile allows to create up to seven variants of the image; that is seven variants of the web app.

The variant images can be used to quickly spawn containers for learning, testing or demonstration purposes.

## App Variants
* black (default)
* blue
* green
* red
* yellow
* purple
* magenta

## Image Build

### Arguments
There are three build arguments:

* `BUILD_DATE` - Used to label the image with the build date of the image (org.label-schema.build-date) (Required)
* `BUILD_VERSION` - Used to label the image with build version (org.label-schema.version)
* `APP_VARIANT` - Used to create the app variant.


### Building a variant
The following command builds the blue image variant:
```Shell
docker build --tag myrepo/nginx:blue --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') --build-arg APP_VARIANT=green .
```

The following command builds the green image variant and specifies a BUILD_VERSION:
```Shell
docker build --tag myrepo/nginx:stable.green --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') --build-arg BUILD_VERSION=1.0 --build-arg APP_VARIANT=green .
```


### Multi-arch build
```Shell
docker buildx build --platform linux/amd64,linux/arm64,linux/ppc64le,linux/s390x,linux/386,linux/arm/v7,linux/arm/v6 --no-cache --rm --tag myrepo/nginx:stable.blue --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') --build-arg BUILD_VERSION=v0.1 --build-arg APP_VARIANT=blue --push .
```

See https://www.docker.com/blog/multi-arch-images/ for how to build multi-arch images.

### Supported Platforms (Archs)
* linux/386
* linux/amd64
* linux/arm64
* linux/arm/v7
* linux/arm/v6
* linux/ppc64le
* linux/s390x