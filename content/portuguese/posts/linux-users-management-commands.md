---
title: "Comandos de Gestão de Usuário no Linux"
date: 2023-07-24T18:46:38
tags: [linux]
slug: "comandos-gestao-usuario-linux"
---

Na tabela abaixo existem alguns comandos que podem ser utilizados para lidar com usuários e grupos:

| Objetivo                                          | Comando                                   |
| --------                                          | -------                                   |
| adicionar usuário                                 | `adduser <username>`                      |
| adicionar grupo de usuário                        | `addgroup <groupname>`                    |
| adicionar grupo de usuário como grupo primário    | `usermod -g <groupname> <username>`       |
| anexar grupo de usuário como grupo suplementar    | `usermod -aG <groupname> <username>`      |
| travar usuário                                    | `usermod -L <username>`                   |
| checar os grupos do usuário                       | `id <username>`                           |
| mudar para usuário root                           | `sudo -i` or `sudo su -`                  |
| mudar para outro usuário                          | `sudo su - <username>`                    |
| configurar senha                                  | `passwd <username>`                       |

Para conceder permissões para um usuário/grupo específico para executar comandos com o _sudo_, isso pode ser apontado em um arquivo _sudoer_ separado (dentro do diretório _sudoers.d_). Há um exemplo abaixo para aplicar configurações para _myuser_ permitindo ele executar os comandos _restart_ e _reload_ do serviço http:

```shell
Cmnd_Alias WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service

myuser ALL=WEB
```

| Objetivo                                                  | Comando                                       |
| --------                                                  | -------                                       |
| abrir arquivo _sudoer_ com seu conteúdo                   | `sudo visudo`                                 |
| criar outro arquivo _sudoer_ para adicionar permissões    | `sudo visudo -f /etc/sudoers.d/<filename>`    |

Alguns comandos para conectar em servidor Linux:

| Objetivo                                  | Comando                                   |
| ----                                      | -------                                   |
| gerar chave SSH                           | `ssh-keygen`                              |
| copiar chave SSH para outro servidor      | `ssh-copy-id <public/private address>`    |
| autenticar usando chave SSH               | `ssh <public/private address>`            |

Comando para copiar arquivos de um servidor para outro com chave SSH:

`scp <files> <private address>:<directory>`

Comando para estabelecer as permissões padrão em um diretório:

```shell
umask XXX
```