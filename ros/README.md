<!--

********************************************************************************

WARNING:

    DO NOT EDIT "ros/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "ros/" combined with a set of templates)

********************************************************************************

-->

# Quick reference

-	**Maintained by**:  
	[the Open Source Robotics Foundation](https://github.com/osrf/docker_images)

-	**Where to get help**:  
	[the Docker Community Slack](https://dockr.ly/comm-slack), [Server Fault](https://serverfault.com/help/on-topic), [Unix & Linux](https://unix.stackexchange.com/help/on-topic), or [Stack Overflow](https://stackoverflow.com/help/on-topic)

# Supported tags and respective `Dockerfile` links

-	[`humble-ros-core`, `humble-ros-core-jammy`](https://github.com/osrf/docker_images/blob/eb5634cf92ba079897e44fb7541d3b78aa6cf717/ros/humble/ubuntu/jammy/ros-core/Dockerfile)

-	[`humble-ros-base`, `humble-ros-base-jammy`, `humble`](https://github.com/osrf/docker_images/blob/20e3ba685bb353a3c00be9ba01c1b7a6823c9472/ros/humble/ubuntu/jammy/ros-base/Dockerfile)

-	[`humble-perception`, `humble-perception-jammy`](https://github.com/osrf/docker_images/blob/20d40c96b426b8956dec203e236abff2ec29b188/ros/humble/ubuntu/jammy/perception/Dockerfile)

-	[`jazzy-ros-core`, `jazzy-ros-core-noble`](https://github.com/osrf/docker_images/blob/eb5634cf92ba079897e44fb7541d3b78aa6cf717/ros/jazzy/ubuntu/noble/ros-core/Dockerfile)

-	[`jazzy-ros-base`, `jazzy-ros-base-noble`, `jazzy`, `latest`](https://github.com/osrf/docker_images/blob/0038f1c3a11aa0fc573d698b39ab5c204aad5a40/ros/jazzy/ubuntu/noble/ros-base/Dockerfile)

-	[`jazzy-perception`, `jazzy-perception-noble`](https://github.com/osrf/docker_images/blob/0038f1c3a11aa0fc573d698b39ab5c204aad5a40/ros/jazzy/ubuntu/noble/perception/Dockerfile)

-	[`kilted-ros-core`, `kilted-ros-core-noble`](https://github.com/osrf/docker_images/blob/eb5634cf92ba079897e44fb7541d3b78aa6cf717/ros/kilted/ubuntu/noble/ros-core/Dockerfile)

-	[`kilted-ros-base`, `kilted-ros-base-noble`, `kilted`](https://github.com/osrf/docker_images/blob/b835a530495c0b411a0d15db858710a2748ee0a0/ros/kilted/ubuntu/noble/ros-base/Dockerfile)

-	[`kilted-perception`, `kilted-perception-noble`](https://github.com/osrf/docker_images/blob/b835a530495c0b411a0d15db858710a2748ee0a0/ros/kilted/ubuntu/noble/perception/Dockerfile)

-	[`rolling-ros-core`, `rolling-ros-core-noble`](https://github.com/osrf/docker_images/blob/8cf2903c0f8813aacd3042c71d4d2d56d5068ad5/ros/rolling/ubuntu/noble/ros-core/Dockerfile)

-	[`rolling-ros-base`, `rolling-ros-base-noble`, `rolling`](https://github.com/osrf/docker_images/blob/8cf2903c0f8813aacd3042c71d4d2d56d5068ad5/ros/rolling/ubuntu/noble/ros-base/Dockerfile)

-	[`rolling-perception`, `rolling-perception-noble`](https://github.com/osrf/docker_images/blob/8cf2903c0f8813aacd3042c71d4d2d56d5068ad5/ros/rolling/ubuntu/noble/perception/Dockerfile)

# Quick reference (cont.)

-	**Where to file issues**:  
	[https://github.com/osrf/docker_images/issues](https://github.com/osrf/docker_images/issues?q=)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/ros/), [`arm64v8`](https://hub.docker.com/r/arm64v8/ros/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/ros/` directory](https://github.com/docker-library/repo-info/blob/master/repos/ros) ([history](https://github.com/docker-library/repo-info/commits/master/repos/ros))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images repo's `library/ros` label](https://github.com/docker-library/official-images/issues?q=label%3Alibrary%2Fros)  
	[official-images repo's `library/ros` file](https://github.com/docker-library/official-images/blob/master/library/ros) ([history](https://github.com/docker-library/official-images/commits/master/library/ros))

-	**Source of this description**:  
	[docs repo's `ros/` directory](https://github.com/docker-library/docs/tree/master/ros) ([history](https://github.com/docker-library/docs/commits/master/ros))

# What is [ROS](https://docs.ros.org/)?

The Robot Operating System (ROS) is a set of software libraries and tools that help you build robot applications. From drivers to state-of-the-art algorithms, and with powerful developer tools, ROS has what you need for your next robotics project. And it's all open source.

> [wikipedia.org/wiki/Robot_Operating_System](https://en.wikipedia.org/wiki/Robot_Operating_System)

[![logo](https://raw.githubusercontent.com/docker-library/docs/0074e9dac72a35e5058f356885121aa82572682f/ros/logo.png)](https://docs.ros.org/)

# How to use this image

## Creating a `Dockerfile` to install ROS packages

To create your own ROS docker images and install custom packages, here's a simple example of installing the C++, Python client library demos using the official released Debian packages via apt-get.

```dockerfile
FROM ros:rolling-ros-core as aptgetter

# install ros package
RUN apt-get update && apt-get install -y \
      ros-${ROS_DISTRO}-demo-nodes-cpp \
      ros-${ROS_DISTRO}-demo-nodes-py && \
    rm -rf /var/lib/apt/lists/*

# launch ros package
CMD ["ros2", "launch", "demo_nodes_cpp", "talker_listener_launch.py"]
```

Note: all ROS images include a default entrypoint that sources the ROS environment setup before executing the configured command, in this case the demo packages launch file. You can then build and run the Docker image like so:

```console
$ docker build -t my/ros:aptgetter .
$ docker run -it --rm my/ros:aptgetter
[INFO] [launch]: process[talker-1]: started with pid [813]
[INFO] [launch]: process[listener-2]: started with pid [814]
[INFO] [talker]: Publishing: 'Hello World: 1'
[INFO] [listener]: I heard: [Hello World: 1]
[INFO] [talker]: Publishing: 'Hello World: 2'
[INFO] [listener]: I heard: [Hello World: 2]
...
```

## Creating a `Dockerfile` to build ROS packages

To create your own ROS docker images and build custom packages, here's a simple example of installing a package's build dependencies, compiling it from source, and installing the resulting build artifacts into a final multi-stage image layer.

```dockerfile
ARG FROM_IMAGE=ros:rolling
ARG OVERLAY_WS=/opt/ros/overlay_ws

# multi-stage for caching
FROM $FROM_IMAGE AS cacher
ARG OVERLAY_WS

# overwrite defaults to persist minimal cache
RUN rosdep update --rosdistro $ROS_DISTRO && \
    cat <<EOF > /etc/apt/apt.conf.d/docker-clean && apt-get update
APT::Install-Recommends "false";
APT::Install-Suggests "false";
EOF

# clone overlay source
WORKDIR $OVERLAY_WS/src
RUN cat <<EOF | vcs import .
repositories:
  ros2/demos:
    type: git
    url: https://github.com/ros2/demos.git
    version: ${ROS_DISTRO}
EOF

# derive build/exec dependencies
RUN bash -e <<'EOF'
declare -A types=(
  [exec]="--dependency-types=exec"
  [build]="")
for type in "${!types[@]}"; do
  rosdep install -y \
    --from-paths \
      ros2/demos/demo_nodes_cpp \
      ros2/demos/demo_nodes_py \
    --ignore-src \
    --reinstall \
    --simulate \
    ${types[$type]} \
    | grep 'apt-get install' \
    | awk '{gsub(/'\''/,"",$4); print $4}' \
    | sort -u > /tmp/${type}_debs.txt
done
EOF

# multi-stage for building
FROM $FROM_IMAGE AS builder
ARG OVERLAY_WS

# install build dependencies
COPY --from=cacher /tmp/build_debs.txt /tmp/build_debs.txt
RUN --mount=type=cache,target=/etc/apt/apt.conf.d,from=cacher,source=/etc/apt/apt.conf.d \
    --mount=type=cache,target=/var/lib/apt/lists,from=cacher,source=/var/lib/apt/lists \
    --mount=type=cache,target=/var/cache/apt,sharing=locked \
    < /tmp/build_debs.txt xargs apt-get install -y

# build overlay source
WORKDIR $OVERLAY_WS
COPY --from=cacher $OVERLAY_WS/src ./src
RUN . /opt/ros/$ROS_DISTRO/setup.sh && \
    colcon build \
      --packages-select \
        demo_nodes_cpp \
        demo_nodes_py \
      --mixin release

# multi-stage for running
FROM $FROM_IMAGE-ros-core AS runner
ARG OVERLAY_WS

# install exec dependencies
COPY --from=cacher /tmp/exec_debs.txt /tmp/exec_debs.txt
RUN --mount=type=cache,target=/etc/apt/apt.conf.d,from=cacher,source=/etc/apt/apt.conf.d \
    --mount=type=cache,target=/var/lib/apt/lists,from=cacher,source=/var/lib/apt/lists \
    --mount=type=cache,target=/var/cache/apt,sharing=locked \
    < /tmp/exec_debs.txt xargs apt-get install -y

# setup overlay install
ENV OVERLAY_WS=$OVERLAY_WS
COPY --from=builder $OVERLAY_WS/install $OVERLAY_WS/install
RUN sed --in-place --expression \
      '$isource "$OVERLAY_WS/install/setup.bash"' \
      /ros_entrypoint.sh

# run launch file
CMD ["ros2", "launch", "demo_nodes_cpp", "talker_listener_launch.py"]
```

The example above consists of three sequential stages. The `cacher` stage first updates the apt lists and ROS index, uses [`vcstool`](https://github.com/dirk-thomas/vcstool) to clone a demo repo into the workspace source directory, and derives build and runtime dependency sets using [`rosdep`](https://docs.ros.org/en/rolling/Tutorials/Intermediate/Rosdep.html). The `builder` stage installs the derived build dependencies, sources the ROS install underlay, and compiles the source in release mode using [`colcon`](https://docs.ros.org/en/rolling/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html). Finally, the `runner` stage installs only runtime dependencies, copies the compiled workspace artifacts, and sets up the environment to launch the demo. Note the example consists of several subtle optimizations:

-	Multi-Stage Build
	-	Dependency derivation, compilation, and runtime setup are partitioned
	-	Maximizes cache retention despite package source or build/runtime changes
	-	Greater concurrency, e.g., colcon build while runtime apt installs
-	Persistent Cache Propagation
	-	Use of [`--mount`](https://docs.docker.com/engine/reference/builder/#run---mount) to cache temp data without bloating layers
	-	Maintain temporally consistent apt lists between parallel stages
	-	Avoid needless network I/O between stages or across Docker rebuilds
-	Minimal Image Size
	-	Final stage builds from `ros-core` for smallest runtime image
	-	Builds and installs only a select few packages in the workspace
	-	Only workspace install artifacts are copied into final layers

For comparison, the resulting `runner` image is similar in size to the earlier `aptgetter` example. This allows you to develop and distribute custom ROS packages without significantly increasing image size compared to pre-built Debian installations:

```console
$ docker image ls my/ros --format "table {{.Tag}}\t{{.Size}}"
TAG                SIZE
aptgetter          504MB
runner             510MB
builder            941MB
$ docker image ls ros --format "table {{.Tag}}\t{{.Size}}"
TAG                SIZE
rolling-ros-core   489MB
rolling            876MB
```

For more advance examples such as daisy chaining multiple overlay workspaces to improve caching of docker image build layers, using tools such as ccache to accelerate compilation with colcon, or using buildkit to save build time and bandwidth even when dependencies change, the project `Dockerfile`s in the [Navigation2](https://github.com/ros-planning/navigation2) repo are excellent resources.

## Deployment use cases

This dockerized image of ROS is intended to provide a simplified and consistent platform to build and deploy distributed robotic applications. Built from the [official Ubuntu image](https://hub.docker.com/_/ubuntu/) and ROS's official Debian packages, it includes recent supported releases for quick access and download. This provides roboticists in research and industry with an easy way to develop, reuse and ship software for autonomous actions and task planning, control dynamics, localization and mapping, swarm behavior, as well as general system integration.

Developing such complex systems with cutting edge implementations of newly published algorithms remains challenging, as repeatability and reproducibility of robotic software can fall to the wayside in the race to innovate. With the added difficulty in coding, tuning and deploying multiple software components that span across many engineering disciplines, a more collaborative approach becomes attractive. However, the technical difficulties in sharing and maintaining a collection of software over multiple robots and platforms has for a while exceeded time and effort than many smaller labs and businesses could afford.

With the advancements and standardization of software containers, roboticists are primed to acquire a host of improved developer tooling for building and shipping software. To help alleviate the growing pains and technical challenges of adopting new practices, we have focused on providing an official resource for using ROS with these new technologies.

For a complete listing of supported architectures and base images for each ROS Distribution Release, please read the official REP on target platforms [here](https://www.ros.org/reps/rep-2001.html).

## Deployment suggestions

The available tags include supported distros along with a hierarchy tags based off the most common meta-package dependencies, designed to have a small footprint and simple configuration:

-	`ros-core`: minimal ROS install
-	`ros-base`: basic tools and libraries (also tagged with distro name with LTS version as `latest`)

In the interest of keeping `ros-core` tag minimal in image size, developer tools such as `rosdep`, `colcon` and `vcstools` are not shipped in `ros_core`, but in `ros-base` instead.

The rest of the common meta-packages such as `desktop` are hosted on repos under OSRF's Docker Hub profile [here](https://hub.docker.com/r/osrf/ros/). These meta-packages include graphical dependencies and hook a host of other large packages such as X11, X server, etc. So in the interest of keeping the official images lean and secure, the desktop packages are just being hosted with OSRF's profile.

### Volumes

ROS uses the `~/.ros/` directory for storing logs, and debugging info. If you wish to persist these files beyond the lifecycle of the containers which produced them, the `~/.ros/` folder can be mounted to an external volume on the host, or a derived image can specify volumes to be managed by the Docker engine. By default, the container runs as the `root` user, so `/root/.ros/` would be the full path to these files.

For example, if one wishes to use their own `.ros` folder that already resides in their local home directory, with a username of `ubuntu`, we can simply launch the container with an additional volume argument:

```console
$ docker run -v "/home/ubuntu/.ros/:/root/.ros/" ros
```

### Devices

Some application may require device access for acquiring images from connected cameras, control input from human interface device, or GPUS for hardware acceleration. This can be done using the [`--device`](https://docs.docker.com/engine/reference/commandline/run/#add-host-device-to-container---device) run argument to mount the device inside the container, providing processes inside hardware access.

### Networks

ROS allows for peer-to-peer networking of processes (potentially distributed across machines) that are loosely coupled using the ROS communication infrastructure. ROS implements several different styles of communication, including synchronous RPC-style communication over services, asynchronous streaming of typed data over topics, combinations of both prior via request/reply and status/feedback over actions, and run-time settings via configuration over parameters. To abide by the best practice of [one process per container](https://docs.docker.com/articles/dockerfile_best-practices/), Docker networks can be used to string together several running ROS processes. For further details see the Deployment example further below.

Alternatively, more permissive network settings can be used to share all host network interfaces with the container, such as [`host` network driver](https://docs.docker.com/network/host/), simplifying connectivity with external network participants. Be aware however that this removes the networking namespace separation between containers, and can affect the ability of DDS participants to communicate between containers, as documented [here](https://community.rti.com/kb/how-use-rti-connext-dds-communicate-across-docker-containers-using-host-driver).

## Deployment example

### Docker Compose

In this example we'll demonstrate using [`docker compose`](https://docs.docker.com/compose/) to spawn a pair of message publisher and subscriber nodes in separate containers connected through shared software defined network.

> Create the directory `~/ros_demos` and add the first `Dockerfile` example from above. In the same directory, also create file `compose.yaml` with the following that runs a C++ publisher with a Python subscriber:

```yaml
services:
  talker:
    build: ./
    command: ros2 run demo_nodes_cpp talker

  listener:
    build: ./
    environment:
      - "PYTHONUNBUFFERED=1"
    command: ros2 run demo_nodes_py listener
```

> Use `docker compose` inside the same directory to launch our ROS nodes. Given the containers created derive from the same docker compose project, they will coexist on shared project network:

```console
$ docker compose up -d
```

> Notice that a new network named `ros_demos_default` has been created, as can be shown further with:

```console
$ docker network inspect ros_demos_default
```

> We can monitor the logged output of each container, such as the listener node like so:

```console
$ docker compose logs listener
```

> Finally, we can stop and remove all the relevant containers using `docker compose` from the same directory:

```console
$ docker compose stop
$ docker compose rm
```

> Note: the auto-generated network, `ros_demos_default`, will persist until you explicitly remove it using `docker compose down`.

# More Resources

[Docs](https://docs.ros.org/): ROS Developer Documentation  
[Q&A](https://robotics.stackexchange.com/): Ask questions. Get answers  
[Forums](https://discourse.ros.org/): Hear the latest discussions  
[Packages](https://index.ros.org/?search_packages=true): Discover indexed packages  
[OSRF](https://www.openrobotics.org/): Open Source Robotics Foundation

# License

View [package index](https://index.ros.org/packages/) for license information on software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `ros/` directory](https://github.com/docker-library/repo-info/tree/master/repos/ros).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
