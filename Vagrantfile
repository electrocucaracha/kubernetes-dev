# -*- mode: ruby -*-
# vi: set ft=ruby :
##############################################################################
# Copyright (c)
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Apache License, Version 2.0
# which accompanies this distribution, and is available at
# http://www.apache.org/licenses/LICENSE-2.0
##############################################################################

$no_proxy = ENV['NO_PROXY'] || ENV['no_proxy'] || "127.0.0.1,localhost"
# NOTE: This range is based on vagrant-libvirt network definition CIDR 192.168.121.0/24
(1..254).each do |i|
  $no_proxy += ",192.168.121.#{i}"
end
$no_proxy += ",10.0.2.15"

Vagrant.configure("2") do |config|
  config.vm.provider :libvirt
  config.vm.provider :virtualbox

  config.vm.synced_folder './', '/vagrant', type: "rsync",
    rsync__args: ["--verbose", "--archive", "--delete", "-z"]
  config.vm.box = "peru/ubuntu-18.04-server-amd64"
  config.vm.box_version = "20200501.01"
  config.vm.provision 'shell', privileged: false do |sh|
    sh.inline = <<-SHELL
      cd /vagrant
      ./installer.sh | tee installer.log
    SHELL
  end

  [:virtualbox, :libvirt].each do |provider|
  config.vm.provider provider do |p, override|
      p.cpus = 4
      p.memory = 16384
    end
  end

  config.vm.provider :libvirt do |v, override|
    v.cpu_mode = 'host-passthrough'
    v.management_network_address = "192.168.124.0/30"
    v.management_network_name = "k8s-mgmt-net"
    v.random_hostname = true
  end

  config.vm.provider "virtualbox" do |v| 
    v.gui = false
  end

  if ENV['http_proxy'] != nil and ENV['https_proxy'] != nil
    if Vagrant.has_plugin?('vagrant-proxyconf')
      config.proxy.http     = ENV['http_proxy'] || ENV['HTTP_PROXY'] || ""
      config.proxy.https    = ENV['https_proxy'] || ENV['HTTPS_PROXY'] || ""
      config.proxy.no_proxy = $no_proxy
      config.proxy.enabled = { docker: false }
    end
  end
end
