# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"
PrestashopPort = 10100
PhpMyAdminPort = 10200

# Vagrant::Config.run do |config|
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # config.vm.forward_port PrestashopPort, PrestashopPort
  # config.vm.forward_port PhpMyAdminPort, PhpMyAdminPort
  config.vm.network :forwarded_port, guest: PrestashopPort, host: PrestashopPort
  config.vm.network :forwarded_port, guest: PhpMyAdminPort, host: PhpMyAdminPort

  config.vm.synced_folder "prestashop", "/var/www/prestashop"

  config.vm.provision :shell, :path => "install_chef.sh" 

  config.vm.provision :chef_solo do |chef|
      chef.provisioning_path = "/etc/chef-solo"
      chef.add_recipe("ak-prestashop")
      chef.json = {
        :prestashop => {
            :port => PrestashopPort,
            :git => "git://github.com/PrestaShop/PrestaShop.git",
            },
        :phpmyadmin => {:port => PhpMyAdminPort},
    }
  end
end
