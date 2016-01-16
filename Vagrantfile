# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  # Bring up the virtualbox gui
  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.memory = 4096
    v.cpus = 2
  end    

  config.vm.synced_folder ".", "/vagrant", mount_options: ["fmode=666"]

  # It's necessary to install ansible manually, as 
  # the ansible_local provisioner installer ansible 2.0, which does not 
  # work with vagrant at the moment.
  config.vm.provision "shell", 
    inline:  "sudo apt-get update &&\
              sudo apt-get -y install python-pip &&\
              sudo pip install ansible==1.9.4 &&\
              ansible-galaxy install --force -r /vagrant/ansible/requirements.txt"

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = false
    ansible.playbook = "ansible/dev-env-playbook.yml"
    ansible.inventory_path = "ansible/inventory"
    ansible.limit = "all"
  end
end
