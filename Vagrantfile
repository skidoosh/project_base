# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"

  config.vm.box_check_update = true
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 4443
  config.vm.synced_folder "./src", "/var/www/src", :id => "vagrant-data",
                                                   :owner => "www-data",
                                                   :group => "www-data",
                                                   :mount_options => ["dmode=775,fmode=664"]

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = 2
    vb.memory = 2048
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.install_mode = "pip"
  end
end
