# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/7"
  config.vm.define "ceos-lab"
  config.vm.hostname = "ceos-lab"

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

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    vb.name = "ceos-lab"
  #   # Display the VirtualBox GUI when booting the machine
    vb.gui = true
  #   # Customize the amount of memory on the VM:
    vb.memory = "5120"
    vb.cpus = "2"
  end
  config.vm.provider "vmware_desktop" do |v|
    v.vmx["memsize"] = "5120"
    v.vmx["numvcpus"] = "2"
    v.vmx["displayName"] = "ceos-lab"
    v.gui = true
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    yum install -y epel-release
    yum -y groupinstall "GNOME Desktop"
    yum install -y terminator
    yum-config-manager \
       --add-repo \
       https://download.docker.com/linux/centos/docker-ce.repo
    yum install -y docker-ce docker-ce-cli containerd.io
    yum install -y git
    yum install -y python3
    yum install -y ansible
    systemctl set-default graphical.target
    systemctl start graphical.target
    systemctl start docker
    docker import --change 'VOLUME /mnt/flash' /vagrant/cEOS-lab*.tar.xz ceosimage:latest
    bash -c "$(curl -sL https://get-clab.srlinux.dev)"
    sudo -u vagrant mkdir /home/vagrant/ceos-lab
    sudo -u vagrant cp /vagrant/*.yml /home/vagrant/ceos-lab/
    sudo -u vagrant cp /vagrant/initial-startup.cfg /home/vagrant/ceos-lab/
    SHELL
end
