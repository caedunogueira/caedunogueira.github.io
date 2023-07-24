---
title: "Linux User Management Commands"
date: 2023-07-24T18:46:38
tags: [linux]
---

In the below table there are some commands can be used to handle users and groups:

| Goal                                      | Command                                   |
| ----                                      | -------                                   |
| add user                                  | `adduser <username>`                      |
| add user group                            | `addgroup <groupname>`                    |
| add specific user group as primary group  | `usermod -g <groupname> <username>`       |
| append user group as suplementary group   | `usermod -aG <groupname> <username>`      |
| lock user                                 | `usermod -L <username>`                   |
| check the user groups                     | `id <username>`                           |
| change to root user                       | `sudo -i` or `sudo su -`                  |
| change to another user                    | `sudo su - <username>`                    |
| set password                              | `passwd <username>`                       |

To give permissions for specific user/group in order to execute commands with _sudo_, it can be pointed out in a separeted _sudoer_ file (within _sudoers.d_ directory). There is a below example to apply settings for _myuser_ enabling it to execute _restart_ and _reload_ commands from http service:

```shell
Cmnd_Alias WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service

myuser ALL=WEB
```

| Goal                                              | Command                                       |
| ----                                              | -------                                       |
| open _sudoer_ file with its content               | `sudo visudo`                                 |
| create another _sudoer_ file to add permissions   | `sudo visudo -f /etc/sudoers.d/<filename>`    |

Some commands to connect to Linux server:

| Goal                                      | Command                                   |
| ----                                      | -------                                   |
| generate SSH key                          | `ssh-keygen`                              |
| copy SSH key to another server            | `ssh-copy-id <public/private address>`    |
| authenticate using SSH key                | `ssh <public/private address>`            |

Command to copy files to one server to another using SSH key:

`scp <files> <private address>:<directory>`

Command to set the default permissions in the directory:

```shell
umask XXX
```