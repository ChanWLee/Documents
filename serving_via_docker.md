# tensorflow serving

## via docker

### set docker
Dockerfile.devel
```dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
        build-essential \
        curl \
        git \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        mlocate \
        pkg-config \
        python-dev \
        python-numpy \
        python-pip \
        software-properties-common \
        swig \
        zip \
        zlib1g-dev \
        libcurl3-dev \
        openjdk-8-jdk\
        openjdk-8-jre-headless \
        wget \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set up grpc

RUN pip install mock grpcio

# Set up Bazel.

ENV BAZELRC /root/.bazelrc
# Install the most recent bazel release.
ENV BAZEL_VERSION 0.5.4
WORKDIR /
RUN mkdir /bazel && \
    cd /bazel && \
    curl -fSsL -O https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VERSION/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    curl -fSsL -o /bazel/LICENSE.txt https://raw.githubusercontent.com/bazelbuild/bazel/master/LICENSE && \
    chmod +x bazel-*.sh && \
    ./bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    cd / && \
    rm -f /bazel/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh

CMD ["/bin/bash"]
```

#### building a container
```bash
$ docker build --pull -t $USER/tensorflow-serving-devel -f Dockerfile.devel .
```

#### running a container
```bash
$ docker run --name=serving -it $USER/tensorflow-serving-devel
```

### git clone in container(docker)
```bash
$ git clone --recurse-submodules https://github.com/tensorflow/serving
$ cd serving/tensorflow
$ ./configure
$ cd ..
$ bazel test tensorflow_serving/...
```

#### build
```bash
$ bazel build -c opt --local_resources 2048,0.5,1.0 --verbose_failures  tensorflow_serving/...
```

#### check
```bash
$ bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server
```
