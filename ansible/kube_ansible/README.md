
# todo

This project is currently in development of an alfa version and in active development

# kube ansible

These ansible roles are meant to be a base setup example to deploy vanilla kubernetes on debian and fedora based systems. The project is specific to on premise setups where we will be using software loadbalancer and ingress controller inside the cluster. We will be using the stacked control plane nodes... todo finish etc and api server vip and add info about them here.

# Requirements

- Linux based systems - debian or fedora based
  - supported package managers
    - apt-get
    - dnf
  - only systemd based linux distributions(sysvinit or openrc are not supported)
  - only glibc based systems are supported
  - no swap - the linux machine must not have swap enabled(we will disable swap if enabled)

# software selection for this project

- external DNS and DHCP servers need to be setup beforehand
  - bind9 for DNS external to the cluster todo see this project for setup
  - isc-dhcp-server for DHCP external to the cluster todo see this project for setup
- container runtime
  - will install containerd, runc, cni plugins, and nerdctl from source for both amd64 and arm64
  - Version seletion via roles/containerd/defaults/main.yaml:containerd_releases dictionary that can be overridden with group_vers in inventory
    - (containerd)[https://github.com/containerd/containerd/releases]
    - (runc)[https://github.com/opencontainers/runc/releases]
    - (cni plugins)[https://github.com/containernetworking/plugins/releases]
    - (nerdctl)[https://github.com/containerd/nerdctl/releases]
- load balancer
  - api-server vip
    - todo
  - PureLB for the cluster services loadbalancer
  - 


# Setting up the inventory

you can create multiple inventory file in the inventory directory. Some things are required for these roles to operate properly.

There must be both the control and worker groups to configure which nodes will be used for the control plane and worker nodes.

Each of those group should have a :vars section to setup the appropriate ansible_user and should also set ansible_become to true.

see the inventory/playground/hosts file for an example of how this can be done. 


# running ansible

There are three main roles with tags...

#TODO complete this section once the playbooks are done.


# laptop or admin VM environment setup to run this ansible

Current newest python version in security release is python 3.11. see python versions [here](https://devguide.python.org/versions/)

```sh
brew install python@3.11;
cd ~;
mkdir .virtualenv
cd ~/.virtualenv
virtualenv -p /opt/homebrew/bin/python3.11 py311
source ~/.virtualenv/py311/bin/activate
pip install ansible
```


# Documentation sources used to build these ansible roles

- (containerd)[https://github.com/containerd/containerd/blob/main/docs/getting-started.md]
- (kubeadm)[https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/]
