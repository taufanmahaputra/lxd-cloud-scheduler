# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
DEFAULT_BOX = "ubuntu/xenial64"
NODE_COUNT = 2
PRESEED = File.read("preseed.yaml")
puts PRESEED

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.define "master" do |subconfig|
    subconfig.vm.box = DEFAULT_BOX
    subconfig.vm.hostname = "master"
    subconfig.vm.provision "shell", inline: <<-SHELL
        echo "Hello from master"
        echo "Running apt install -qq -y -t xenial-backports lxd lxd-client"
        sudo apt install -qq -y -t xenial-backports lxd lxd-client
        echo "Running apt-get -qq -y install zfs"
        sudo apt-get -qq -y install zfs
        echo "#{PRESEED}"
        echo "#{PRESEED}" | lxd init --preseed
    SHELL
  end

  (1..NODE_COUNT).each do |i|
    config.vm.define "node-#{i}" do |subconfig|
      subconfig.vm.box = DEFAULT_BOX
      subconfig.vm.hostname = "node-#{i}"
      # To add: --preseed
      subconfig.vm.provision "shell", inline: <<-SHELL
        echo "Hello from node #{i}"
        echo "Running apt install -qq -y -t xenial-backports lxd lxd-client"
        sudo apt install -qq -y -t xenial-backports lxd lxd-client
        echo "Running apt-get -qq -y install zfs"
        sudo apt-get -qq -y install zfs
        echo "#{PRESEED}"
        echo "#{PRESEED}" | lxd init --preseed
      SHELL
    end
  end

  config.vm.network "private_network", type: "dhcp"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    vb.memory = 1024
    vb.cpus = 2
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs 
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
