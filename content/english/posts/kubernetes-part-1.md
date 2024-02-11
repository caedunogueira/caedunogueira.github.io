---
title: "Kubernetes - Part 1"
date: 2024-02-11T10:30:00-03:00
tags: [kubernetes]
---

Kubernetes is a container orchestrator thought to run using a container architecture, that is, a cluster containing a master node (the control plane node) and slave nodes (the working nodes). A control plane node is only responsible for managing the working nodes and ensuring their health to run their workloads. The control plane node won't have any workload running on it due to getting more robust and efficient, increasing the chances of avoiding a problem occurring on it due to a workload problem.
The control plane node will expose its API, which enable to manage and interact with the cluster.

On the other hand, the working node will be responsible for running all workloads in that cluster. Workloads mean all of the structure/objects that are part of Kubernetes in addition to application containers. Working nodes are virtual machines allocated as nodes to be part of the cluster. The difference between virtualization in a virtual machine and virtualization in a container is that virtualization in a virtual machine occurs at the hardware level, whereas virtualization in a container occurs at the operating system level.

Container is an operating system process that uses system resources and makes syscalls to the kernel managed by the container engine. The container engine is responsible for applying limits to that process in terms of resource usage and allowing which syscalls to send to the kernel. That process (container) and its children are isolated from the rest of the operating system as an approach known as namespace.

Each container represents an image in execution. A container image is a definition of an environment in a reading format.

The working node state represents a set of data regarding the workloads running on that node, like the number of workloads, the environment variables passed to it, name, version, and so on.

To manage the cluster, the API in the control plane node needs a lot of information from working nodes. But, at the same time, the purpose of the API is to become simply enough, and it is not possible in terms of complexity where each node has a way to extract some data or run some commands, for example. To keep in mind a simple API, another component comes to the scene to help with the management of the cluster. It is called __kubelet__.

Kubelet is a component for working nodes that receives commands from the API to run there and to get the data necessary for the control plane to assess the node state, know more about their workloads, and so on.

## Pod

Pod is the smallest deployable resource on the working node. Pod is an abstraction of the process running on a cluster and is able to contain a set of containers.
Even though a pod can represent a set of containers, most of the time it is more of an exception scenario than a rule because if you have some applications running on the same pod and there is a problem with it, all of those applications will be unavailable.


There is a scenario where someone can be motivated to group containers into one pod, like one component wouldn't exist without another, as a strong coupling. Except that, the idea (or will face with) will be one container per pod.


All processes running within a pod will share the same resources, like CPU, memory, volume, network, and so on, similar to a virtual machine. At the same time, all of the processes can communicate with one another via localhost because they are on the same network. Outside the pod, all of them will have the same IP address but a different port. So, if you have one container on port X, you don't have another container using the same port.


Pods are __ephemerals__. It means that they shouldn't be considered as persistent.

### Resources

Thinking about working nodes as machines with scarce resources, the Pod manifest file has a key called __resources__ that enables you to set the minimum and maximum use of CPU and memory for that container. Establishing these settings is considered a good practice due to the scarce resources available on nodes.


The key __resources__ has two other keys called __requests__ and __limits__. Each of them can use the keys, __cpu__, and __memory__ to provide the required resources, either the maximum ones to use or the minimum ones.


For the key __CPU__, the value 1 represents 100% of CPU usage. It is the same as 1000m (milicores).
For the key __memory__, the value is in bytes, followed by one of the available units (E, P, G, M, and K).

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-name
spec:
  containers:
    - name: my-container-name
      image: my-container-image
      resources:
        requests:
          cpu: 100m
          memory: 150M
        limits:
          cpu: 400m
          memory: 550M
      ports:
        - containerPort: 8080
```

When the control plane node receives an order to create a new pod, it doesn't mean the pod will be created at the same time because the process the control plane node will take is to schedule this event because it is necessary to assess if there is a node able to allocate that pod with respect to resource limits established for that pod. You won't receive an error with the create command, but keep in mind that sometimes it won't occur at the same time.


The control plane node will get the remaining CPU and memory available on the node (difference between CPU and memory availables and CPU and memory allocated for all workloads in all namespaces) and compare it to the resource limits established for the new pod. The API will follow the next steps only if there is one node able to allocate it. On the other hand, it keeps the pod state pending.
Using the command `kubectl describe pod <pod-name>` helps to see the list of events that occurred to that pod, including the ones between the scheduling step and creating one.

### Graceful shutdown

The pod is considered ephemeral. Other workloads that do not have a volume attached to them have the same characteristic. When you apply the command `kubectl delete pod <pod-name>`, the API waits a period, the default is 30 seconds, for the pod to terminate its execution. In disrespect to that time, the API sends a SIGNKILL sign to force terminate its execution. The grace period can be changed by the flag `--grace-period`. To delete Pod without waiting that time, the flag `-f` can be used.

```shell
kubectl delete pod <pod-name> --grace-period=<number>
```

```shell
kubectl delete pod <pod-name> -f
```