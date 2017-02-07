# -*- mode: ruby -*-
# vi: set ft=ruby :

DOMAIN="local"
servers=[
  {
    :hostname => "web1." + DOMAIN,
    :ram => 500
  },
  {
    :hostname => "web2." + DOMAIN,
    :ram => 500
  },
  {
    :hostname => "web3." + DOMAIN,
    :ram => 500,
  },
  {
    :hostname => "web4." + DOMAIN,
    :ram => 500,
  }
]
 
Vagrant.configure(2) do |config|
    config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y apache2
    SHELL
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = "ubuntu/trusty64"
            node.vm.hostname = machine[:hostname]
            node.ssh.password = "vagrant"
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
                vb.name = machine[:hostname]
                if (!machine[:hdd_name].nil?)
                    # Не создавать диск, если он уже существует
                end
            end
        end
    end
end

