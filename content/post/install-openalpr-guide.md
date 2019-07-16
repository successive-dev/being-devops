---
title: "Install Openalpr Guide"
date: 2019-07-16T11:34:13+05:30
draft: false
tags: ["openalpr","installation","ubuntu","fedora", "linux", "docker"]

---

Openalpr a fantastic piece of technology leveraging the use of neural networks and machine learning, and above all its open source means you can play with it, convert it into a meaningful product, etc.

Installing it can be a pain in the a**. So here in this blog, I will write some ways you can install it easily, For now, I am talking about only one way in which you can do it and I will update other ways later.

## Using Docker

The software comes with a Dockerfile, which can be used to create an Image and have the software running. So it's the easiest way to install Openalpr ;)

### Pre-requisites

Pre-requisites for moving ahead on this path, you will need to download the docker and enable hypervisor-V in your bios settings. (Docker needs hypervisor-V to run)

#### Clone the git-repo

```shell
$git clone https://github.com/openalpr/openalpr.git
$cd openalpr
```

#### Build Image

```shell
$docker build -t openalpr .
```

#### Run Openalpr

```shell
# Download test image
$wget http://plates.openalpr.com/h786poj.jpg

# Run alpr on image
$docker run -it --rm -v $(pwd):/data:ro openalpr -c eu h786poj.jpg
```

You can find same instructions on their official Github repo
https://github.com/openalpr/openalpr#docker
