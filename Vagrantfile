# -*- mode: ruby -*-
# vi: set ft=ruby :

# check for the presence of the vagrant-vbguest plugin which automatically
# updates the VB guest tools in the VM.
unless Vagrant.has_plugin?("vagrant-vbguest")
  raise 'run "vagrant plugin install vagrant-vbguest" first.'
end  

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  #config.vm.box = "npalm/mint17-amd64-cinnamon"
  config.vm.box = "test"	
  # We don't want to install the guest additions automatically as 
  # X windows wont be installed yet.
  config.vbguest.auto_update = false

  # Bring up the virtualbox gui
  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.memory = 4096
    v.cpus = 2
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    v.customize ["modifyvm", :id, "--hwvirtex", "on"]
    v.customize ["modifyvm", :id, "--accelerate2dvideo", "on"]
    v.customize ["modifyvm", :id, "--accelerate3d", "on"]
    v.customize ["modifyvm", :id, "--vram", "256"]
  end    

  config.vm.synced_folder ".", "/vagrant", mount_options: ["fmode=666"]

  # It's necessary to install ansible manually, as 
  # the ansible_local provisioner installer ansible 2.0, which does not 
  # work with vagrant at the moment.
$script = <<'EOF'
ansible-galaxy install --force -r /vagrant/ansible/requirements.txt
EOF
  config.vm.provision "shell", inline: $script 

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = false
    ansible.playbook = "ansible/dev-env-playbook.yml"
    ansible.inventory_path = "ansible/inventory"
    ansible.limit = "all"
  end
end
