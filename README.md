# Kubernetes Development Environment
[![Build Status](https://travis-ci.org/electrocucaracha/kubernetes-dev.png)](https://travis-ci.org/electrocucaracha/kubernetes-dev)

## Summary

This project offers an automated way to setup a Virtual Machine to
build the [Kubernetes source code][1]. This has been created for
didactic purposes and it's not targeting to replace any community
process.

## Setup

This project uses [Vagrant tool][2] for provisioning Virtual Machines
automatically. It's highly recommended to use the  *setup.sh* script
of the [bootstrap-vagrant project][3] for installing Vagrant
dependencies and plugins required for its project. The script
supports two Virtualization providers (Libvirt and VirtualBox).

    $ curl -fsSL https://raw.githubusercontent.com/electrocucaracha/bootstrap-vagrant/master/setup.sh | PROVIDER=libvirt bash

Once Vagrant is installed, it's possible to deploy the demo with the 
following instruction:

    $ vagrant up

[1]: https://github.com/kubernetes/kubernetes
[2]: https://www.vagrantup.com/
[3]: https://github.com/electrocucaracha/bootstrap-vagrant
