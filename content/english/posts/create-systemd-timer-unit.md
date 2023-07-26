---
title: "Create a Systemd Timer Unit"
date: 2023-07-26T18:30:00
tags: [linux]
---

In order to schedule an execution for a specific service given a period of time, a timer file can helps achieve this goal. Timers are systemd unit files, in which its name is followed by the suffix __.timer__, and it has that characteristic. Look into to its file content as demonstrated in the following example, we can notice the presence of section __Timer__:

```shell
[Unit]
Description=XXXX

[Timer]
OnCalendar=*-*-* 10:30:00
Persistent=true
Unit=<service file>

[Install]
WantedBy=<target>
```

The __Timer__ section uses the option __OnCalendar__ to establish when the service should be executed (in the above example, always at 10:30) pointing out to its service in the option __Unit__.

Nonetheless, as a user-defined unit, both timer and service files need to be available in the _/etc/systemd/system/_ directory so, the target specified in both files will be able find out them and it is able involves them into the Linux system startup process.

Afterwards, the next step is to run the `daemon-reload` command to recalculate the service dependencies, enable them in order to create symbolic link from target systemd directory to systemd directory in which they are available and lastly, start them. The following example bring the sequence of those commands:

```shell
systemctl daemon-reload
systemctl enable <timer file> <service file>
systemctl start <timer file> service file>
```

You can see their status using the below commands:

```shell
systemctl status <timer file>
systemctl status <service file>
```