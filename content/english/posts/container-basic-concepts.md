---
title: "Container Basic Concepts"
date: 2023-10-08T12:08:41-03:00
tags: [container]
---

## Virtual Machines and Containers

One approach to deploying software as a portable solution is to use virtual machines. The virtual machines are able to emulate the proper operating system needed for that application, running on top of the host operating system in that bare metal. However, it considers a high usage of the host resources that leverage the costs. Another point to bring to the discussion as another example is about scaling the applications. It’s neither simple nor fast to provide another application instance due to the time to boot a new virtual machine, that is, the time to spin up another replica of that operating system along with the required components there. On the one hand, you can provision a virtual machine running an operating system, regardless of the host operating system. On the other hand, costs and scalability are tough to deal with.

The other approach to deploying software as portable solutions is to use Containers. The slight difference from Virtual Machines is that the isolated environment will use kernel resources directly from the host operating system. By doing this, Containers are considered smaller, cheaper, and faster than Virtual Machines, because you are able to spin up more instances on the same host (due to consuming fewer resources than Virtual Machines) and those instances are provided in terms of seconds instead of minutes. On the one hand, you have the advantages mentioned in the last sentence; on the other hand, it is less portable than Virtual Machines. For example, you can have Linux containers running on top of the host operating system as Windows, but the opposite is not possible, that is, Windows containers running on top of the host operating system using Linux.

## Orchestration

Nowadays, complex software in the production environment needs to use scalability and elasticity in order to handle all the traffic in a proper way, taking advantage of the best choices in resource usage (costs) and performance. To achieve that goal, one way is to use an orchestration tool like Kubernetes. Those tools help us with many activities that were done manually in the past, like downtime deployment or such application instances presenting problems during execution.

### Zero-Downtime Deployment

In a scenario to upgrade the application version in a production environment, you face the challenge of minimizing the impact the upgrade process can have on it, choosing the better approach to decrease as much as possible the time in which the server would take to apply those changes. An example to illustrate it is about to apply the changes to the environment in a period of time that has the fewest consumptions for the application. Sometimes the process can provide an unforeseen situation, like problems with a new version, for which it is necessary to step back, adopt a rollback plan for the current version, and make an assessment to understand what happened.

An orchestration tool contains an approach to overcome this problem, considering zero-downtime deployment of the process. As an automated task, based on the metrics collected, it is possible to spin up new containers with the newest application version while keeping the old containers with the current version. Throughout the process, the tool will transfer the traffic, little by little or at a rhythm chosen by the responsible person, from the old containers to the new ones. The old containers will be removed only if, according to the metrics presented, there were no problems with the new application version in the new containers. The newest containers will take the place of the old ones. All of it without human interference in the process.

### Self-healing applications

Based on metrics, when an orchestration tool identifies one container with problems, it is easy for it to automatically replace the problematic container with the healthy one. All of those steps are made by the tool automatically, providing more resilience to the application. The replacement takes a few seconds. This approach in which the tool takes this type of decision (based on some settings established by someone, of course) without human interference is called self-healing, that is, the process where the application will “fix” itself in the environment.

## History

In the 1970s, Mainframe computers were a scarce resource for businesses due to their cost. This leads to the development of centralized computers and the sharing of resources among multiple users.

In 1979, the first step towards a containerization solution was to use the chroot command. The chroot command changes root. It changes the apparently root directory of a process and all of its children processes. It means that the process and all of the child processes spun up from it are limited to viewing the file structure only from that chrooted environment.

In the 1990s, Bill Cheswick wanted to build an environment that allowed him to study crackers keystrokes in order to trace him and learn his techniques. His solution was to use a chrooted environment and begin to make modifications. The result would be what we have come to know today as the Linux jail command.

On March 4, 2000, FreeBSD introduced the FreeBSD jail command into its operating system. Although it was similar to the chroot command, it also included additional process sandboxing features for isolating the filesystem, users, networking, etc. It provided more control over these isolated environments.

In 2006, Enginners at Google announced process containers designed for isolating and limiting the resource usage of a process. In 2007, these process containers were renamed Control groups (Cgroups) to avoid confusion with the word container. They were later adopted into the Linux kernel and enabled the development of some technologies, like LXC. LXC stands for Linux Containers and provides operating system level virtualization by allowing multiple isolated Linux environments (containers) to run on a shared Linux kernel.

There were other groups of people studying about better approaches to managing their clusters. In 2009, Mesos began as a research project in the UC Berkeley RAD lab and was first presented by Nexus. The name Nexus conflicted with another university project and was changed to Mesos.

In 2013, using LMCTFY, applications could be written to be container aware and thus programmed to create and manage their own sub-containers. Docker was released as an open source project in 2013. Docker helped provide the ability to package containers so that they could be moved from one environment to another. Docker Swarm v1.0 was released on November 3, 2015. Swarm allows Docker applications to be run at scale on a cluster. Kubernetes is an open-source container orchestration system that was heavily influenced by Google’s Borg system. It was announced in mid-2014, with Kubernetes v1.0 being released on July 21, 2015.

Docker Swarm provides cluster management and orchestration functionality, allowing containers to be run on a cluster of machines.

To avoid any confusion with the usage of the term containers, __process contaneirs__ were renamed __Control groups__, or __Cgroups__.