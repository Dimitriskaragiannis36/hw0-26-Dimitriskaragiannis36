[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/lC2Bak7u)
# Homework #0 2026

Topics: Github, Packages, Actions, Docker, Python, Bash, Buffer Overflows

## Write up of our first exploit (25 Points)

[iwconfig](https://www.geeksforgeeks.org/linux-unix/iwconfig-command-in-linux-with-examples/) is a popular utility for configuring your wireless connection in Linux. It's written in C - thus extremely lightweight - and thus ideal for low-powered devices. Unfortunately, updating some of these devices is pretty time-consuming and sometimes older versions of iwconfig remain in production. Recently, we spotted one of these older versions [online](https://hub.docker.com/r/ethan42/iwconfig) - is the container `ethan42/iwconfig:vulnerable` safe to use?

We suspect no, but we need someone to demonstrate it. Luckily, it seems that part of the code that was used to compile it is available within the container (`/workdir/iwconfig.c`). If you feel the need, you may be able to recover more of it online!

### Requirements

Your mission, should you choose to accept it, is to:

1. Write up and commit an `exploit.py` script runnable in python3 that produces an exploit payload for iwconfig. We need the payload to spawn a root shell when sent to iwconfig. The `exploit.py` script should be committed to the top-level directory of the repo.
1. Add a `writeup.md` file and provide a detailed write up of how you managed to exploit this program. Include a successful invocation in your write up. Detailed write ups will result in higher grades.

An example successful invocation follows:

```
$ docker run --rm --privileged -v `pwd`/exploit.py:/exploit.py -it ethan42/iwconfig:vulnerable
ubuntu@c9ac1746c338:~$ iwconfig
lo        no wireless extensions.

eth0      no wireless extensions.

ubuntu@c9ac1746c338:~$ iwconfig foo
foo       No such device

ubuntu@c9ac1746c338:~$ python3 /exploit.py > payload
ubuntu@c9ac1746c338:~$ whoami
ubuntu
ubuntu@c9ac1746c338:~$ iwconfig `cat payload`
# whoami
root
#
```

## Running our first devsecops pipeline (25 Points)

Some vulnerabilities are known and some are unknown. In this part of the homework, we will develop a continuous integration pipeline to scan docker containers for *known* vulnerabilities. Specifically, we will be using [Github Actions](https://github.com/features/actions) as the CI system and [docker scout](https://docs.docker.com/scout/) as the underlying scanner.

The end goal is to produce a successfully [pipeline run similar to this one](https://github.com/ethan42/sbom-sca-scanner/actions/runs/22440636796) for a docker image within your Github Container Registry (ghcr.io). You can use this [template repository](https://github.com/ethan42/sbom-sca-scanner/) if you are not sure where to start.

### Requirements

As part of this exercise, you have to:

1. Create a public repository in your personal Github workspace and perform a successful scan for a docker image in your ghcr.io image registry. Build a docker image that will be different than what others choose (ideally a personal project) since we will be using Dockerfile contents to detect copy-paste issues from others :)
1. Commit in this repo a `successful_run.txt` file (again in the top-level folder of the repo) that includes the URL of your GitHub action successfully running on a docker image and identifying vulnerabilities. For example, ethan42 can use "https://github.com/ethan42/sbom-sca-scanner/actions/runs/22440636796" as the URL for a successful run on the image [ghcr.io/ethan42/sbom-sca-scanner:latest](https://github.com/ethan42/sbom-sca-scanner/pkgs/container/sbom-sca-scanner).

