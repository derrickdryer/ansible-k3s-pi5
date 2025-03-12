# Automated K3S Cluster with VIP

This ansible playbook automatically creates a simple K3S cluster on a cluster of 3 raspberry pi 5s.

## Prerequisite

1. Enable cgroups on your Raspberry Pi 5s

`sudo nano /boot/firmware/cmdline.txt`

Add this to the end and do not make a new line:

`cgroup_memory=1 cgroup_enable=memory`

2. (Recommended) Generate an ssh key on your workstation and add it to each node in the cluster

`ssh-keygen -t ed25519 -C "Your comment here"`

`ssh-copy-id -i ~/.ssh/id_ed35519.pub username@host`
