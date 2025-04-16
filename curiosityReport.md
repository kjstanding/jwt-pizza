# Linux Kernel & Docker Containers
- Lorem Ipsum.

## Motivivation
I recently decided to learn how to self-host and manage applications on a server at home. In order to learn, I jumped into the process of installing a Linux distro on an extra computer to host a couple applications from. After lots of trial and error, I got a portfolio site and a minecraft server up and running. When we got to the Docker/containers part of the class I realized how great an addition Docker would make to my server. Thus, I decided to take the suggestion to dig into the Linux Kernel's support for Docker Containers.

## Researching
### Namespaces
The linux kernel uses namespaces in order to identify and provide isolation to running processes. Containers are essentially just a process and run with a number of different kinds of namespaces that create isolation from the container's host and other containers. These are described in "Understanding 7 concepts of containers" by David Mosyan on Medium:
- **Processes**: The container’s main process is the parent of others within the container. All these processes share the same process namespace.
- **Network**: Each container receives a network stack with unique interfaces and IP addresses. Processes (or containers) sharing the same network namespace will get the same IP address. Communications between containers pass through host bridge interfaces.
- **Users**: Users within containers are unique; therefore, each container gets its own set of users, but these users are mapped to real host user identifiers.
- **Inter-process communication (IPC)**: Each container receives its own set of shared memory, semaphores, and message queues so that it doesn’t conflict with other processes on the host.
- **Mounts**: Each container mounts a root filesystem; we can also attach remote and host local mounts.
- **Unix time-sharing (UTS)**: Each container is assigned a hostname and the time is synced with the underlying host.

### CGroups
A cgroup allows us to limit available cpu, memory, and other hardware resources to processes and thus containers. This enables us to split up our resources amongst different containers and make it so that a single container will not hog up all the resources and crash other containers.

### Kernel Capabilities
The permissions that a process has on the system kernel are compartmentalized into "capabilities". Container processes are given limited kernel capabilities, improving security and isolation of containers from the host.

### Light-weight containers
VMs virtualize even the OS kernel, thus each VM has its own kernel. Containers use the host kernel, significantly reducing complexity and overhead and helping containers to be much more light-weight.

## Conclusion
I would love to dive even deeper into kernels and what exactly they do. My deep dive into what containers leverage from the linux kernel gives me a good jumping point to learn more. I also will likely containerize my applcations in my home server and play around to learn more about the kernel and containers.