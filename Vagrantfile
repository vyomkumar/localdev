# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.5"
PLUGINS = %w(vagrant-auto_network)
PLUGINS.reject! { |plugin| Vagrant.has_plugin? plugin }

unless PLUGINS.empty?
  print "The following plugins will be installed: #{PLUGINS.join ", "} continue? [Y/n]: "
  unless ['no', 'n'].include? $stdin.gets.strip.downcase
    PLUGINS.each do |plugin|
      system("vagrant plugin install #{plugin}")
      puts
    end
  end
  puts "Please run again"
  exit 1
end

AutoNetwork.default_pool = '172.16.0.0/24'

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.3"
  # config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "forwarded_port", guest: 80, host: 8083
  config.vm.synced_folder ".", "/vagrant", id: "bootstrap", type: "virtualbox"
  # config.vm.synced_folder "./code", "/home/vagrant", id: "code", type: "virtualbox"
  config.vm.hostname = "localdev"
  config.vm.network "private_network", type: "dhcp"
  # config.vm.network "private_network", auto_network: "true"
  config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "site.yml"
  end
end