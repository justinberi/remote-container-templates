# Remote-Container Templates

This repo houses a bunch of examples for using [VS Code Remote Containers](https://code.visualstudio.com/docs/remote/containers).

The project structure is purposefully kept flat  and simple with minimal inheritance so that anyone can start from a bare container and build up.

# Setup

1. Install [Docker](https://docs.docker.com/get-docker/) and add the host user to the docker group (usually requires a restart).

1. Install `nvidia-container-runtime` to access your nvidia graphics card. If it's not already listed in apt-get then use the [official install instructions](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).

1. Install [VSCode](https://code.visualstudio.com/).

1. Install the [Remote-Containers](https://code.visualstudio.com/docs/remote/containers) extension in VS Code.

1. Open the desired folder in VS Code and build and run the remote container with `F1` -> `Remote-Containers: Rebuild and Reopen in Container`.