# Automated K3S Cluster with VIP

This ansible playbook automatically creates a simple K3S cluster on a cluster of 3 raspberry pi 5s.

## Prerequisite

1. Enable cgroups on your Raspberry Pi 5s

	`sudo nano /boot/firmware/cmdline.txt`

	Add this to the end and do not make a new line:

	`cgroup_memory=1 cgroup_enable=memory`

2. (Recommended) Generate an ssh key on your workstation and add it to each node in the cluster

	```bash
	ssh-keygen -t ed25519 -C "Your comment here"
	ssh-copy-id -i ~/.ssh/id_ed35519.pub username@host
	```

3. Create a kubeconfig folder on worksation:

	```bash
	mkdir ~/.kube && touch ~/.kube/config
	```

## Deploying the cluster

Make sure you configure the following files:

- inventory.ini

- k3s-ha-cluster.yml

- templates/keepalived.conf.j2

Once you have fully configured everything you can just run:

`ansible-playbook -i inventory.ini k3s-ha-cluster.yml --ask-become-pass`

And then enter your sudo password, unless you are using passwordless sudo then you can ommit that.

## After deployment

In order to be able to properly connect to the K3S cluster from your workstaton you need to configure the IP:PORT in your local .kube/config

`nano ~/.kube/config`

This is found at the top of the config

```txt
clusters:
- cluster:
    certificate-authority-data: [SECRET]
    server: https://[CHANGEME]:6443
  name: default
```
