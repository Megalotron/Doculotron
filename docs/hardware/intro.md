---
sidebar_position: 1
---

# Jetson Nano

## Operating System

The operating system is the one provided by nvidia, an ubuntu 18.04 available here: [https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#write](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#write)

## Setup

### Docker

We first need to install docker and add our user to the docker group in order to not have to use sudo to run any docker command

### SSH

We need to setup the SSH so that we can connect whenever we need and without password authentication, only a publickey authentication, this configuration is in the file `/etc/ssh/sshd_config`.
We also need to enter everyone’s public keys into the `~/.ssh/authorized_keys` so that everyone can access the jetson

For now, we have a big issue with SSH.
The initial situation was: we could connect from a computer once and after closing the SSH connection, it would spit “connection refused” on every other try.
The actual situation is the following: we can connect multiple times in a row after closing previous connections but after a while we start getting “connection refused” messages.
The solution used at the moment is one provided by jetson nano users on an nvidia forum ([https://forums.developer.nvidia.com/t/unable-to-ssh-into-jetson-nano-through-ethernet/72639/8](https://forums.developer.nvidia.com/t/unable-to-ssh-into-jetson-nano-through-ethernet/72639/8)) and we need to find the root cause of this issue to be able to entirely fix it.

### Git / Github

We need to generate SSH keys and add the publickey to the github organization so that the jetson can clone the repositories.

## Configuration

### Shell

The shell used is ZSH with Oh-My-Zsh ([https://ohmyz.sh/](https://ohmyz.sh/)) and PowerLevel10k ([https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)).
The whole other shell aliases and stuff like that are my personal configuration.
Some aliases do not work since the programs called aren’t installed and I didn’t bother looking too much for them for now since it’s just QoL stuff and having the SSH working is more important right now.