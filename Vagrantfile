
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.hostname = "docker-host"
    config.vm.network "private_network", type: "dhcp"
  
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
  
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision.yaml"
      ansible.inventory_path = "inventory.yaml"
    end
  end
  