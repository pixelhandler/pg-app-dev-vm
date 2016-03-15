# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION="2"

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  #config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64"
  config.vm.host_name = "postgresql"

  # Configurate the virtual machine to use 2GB of RAM
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  # PostgreSQL Server port forwarding
  # Forward the Rails server default port to the host
  config.vm.network :forwarded_port, guest: 5432, host: 54322

  config.vm.network :public_network, :bridge => "en0: Wi-Fi (AirPort)"
  # use `ifconfig` to find ip after `vagrant ssh`, or set an IP:
  # config.vm.network "private_network", ip: "192.168.50.4"

  config.ssh.forward_agent = true

  config.vm.provision :shell, inline: $script
  config.vm.provision :shell, :path => "Vagrant-setup/bootstrap.sh"
end
