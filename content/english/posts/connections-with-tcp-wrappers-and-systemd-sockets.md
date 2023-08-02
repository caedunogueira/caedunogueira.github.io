---
title: "Connections with TCP Wrappers and Systemd Sockets"
date: 2023-08-02T07:30:13
tags: [linux]
---

You can create an extra layer for connections using Systemd Sockets with TCP Wrappers. Firstly, we need check the `sshd.socket` is stopped:

```shell
systemctl status sshd.socket
```

Otherwise, we can use the below command to achieve this goal.

```shell
systemctl stop sshd.socket
```

The next step could be create a job to stop `sshd.service` and start `sshd.socket`. The following commands help in this task:

```shell
sudo at now + 3 minutes
at > systemctl stop sshd.service
at > systemctl start sshd.socket
```

The command `Ctrl + D` will allow finish the edition and schedule the job for the proposal time. Afterwards the Systemd Socket has been started, you can check the presence of TCP Wrapper library:

```shell
ldd /usr/sbin/sshd | grep libwrap
```

The last step is allow and deny connections to the host to only allow sshd socket connections. Open the file `/etc/hosts.allow` to append the line `sshd2 sshd : ALL`. The next file to make changes is `/etc/hosts.deny` with the instruction `ALL : ALL`.