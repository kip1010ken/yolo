# Vagrantfile
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "docker-host"
    config.vm.network "private_network", type: "dhcp"
  
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2024"
      vb.cpus = 1
    end
  
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision.yml"
    end
  end
  