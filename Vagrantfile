# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "7.3.22.4"
  config.vm.hostname = "terra"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  # Provision:
  config.vm.provision "shell", path: "https://raw.githubusercontent.com/terra-ops/terra-cli/master/install.sh"


  config.vm.provision "shell", inline: <<-SHELL
    # Add user to docker group
    usermod -aG docker vagrant

    # Generate keygen for user "vagrant"
    su vagrant -c 'ssh-keygen -t rsa -N \"\" -f ~/.ssh/id_rsa'

    # Install RabbitMQ (from https://github.com/albatrossdigital/terra_ui)
    echo "deb http://www.rabbitmq.com/debian/ testing main"  | tee  /etc/apt/sources.list.d/rabbitmq.list > /dev/null
    wget http://www.rabbitmq.com/rabbitmq-signing-key-public.asc
    apt-key add rabbitmq-signing-key-public.asc
    apt-get update
    apt-get install rabbitmq-server -y
    service rabbitmq-server start
    rabbitmq-plugins enable rabbitmq_management
    service rabbitmq-server restart

    # Install terra-callback
    git clone https://github.com/albatrossdigital/terra-callback /usr/share/terra-callback
    cd /usr/share/terra-callback
    composer install
    # php receiver.php

  SHELL
end
