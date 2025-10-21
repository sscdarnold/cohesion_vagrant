# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "bento/almalinux-9"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :parallels do |par|
    par.memory = 1024
    par.cpus = 2
  end
  config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
  config.vm.define "web0" do |web|
    web.vm.network "private_network", ip: "10.211.56.120" 
  end
  config.vm.define "web1" do |web|
    web.vm.network "private_network", ip: "10.211.56.121" 
  end
  config.vm.define "web2" do |web|
    web.vm.network "private_network", ip: "10.211.56.122" 
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "web_boxes.yml"
    ansible.compatibility_mode = "auto"
    ansible.groups = {
      "web" => ["web0", "web1", "web2"]
    }
  end
end
