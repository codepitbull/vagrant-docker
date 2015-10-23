VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.7.4"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64-juju"
  config.vm.box_check_update = true
  config.vm.network "forwarded_port", guest: 80, host: 80
#  config.vm.provision "docker", version: "1.8" do |docker|
#    docker.pull_images "ubuntu"
#  end
  config.vm.provider "virtualbox" do |vm|
    vm.memory = 2048
    vm.cpus = 2
    vm.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vm.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "docker.yml"
  end
  Vagrant.configure("2") do |config|
    config.vm.synced_folder "share/", "/share", create=true  
  end
end


