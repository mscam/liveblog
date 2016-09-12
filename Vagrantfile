# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/opt/superdesk"

  # config.vm.network "forwarded_port", guest: 8080, host:8080
  # config.vm.network "forwarded_port", guest: 9000, host:9000
  config.vm.network "forwarded_port", guest: 5000, host:5000
  config.vm.network "forwarded_port", guest: 5100, host:5100

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.provisioning_path = "/opt/superdesk/ansible"
    ansible.playbook = "dev.yml"
  end

  config.vm.provision "shell", inline: "printf 'localhost\n' | sudo tee /etc/ansible/hosts > /dev/null"

  config.vm.provider "vmware_fusion" do |vf|
    vf.gui = false
    vf.vmx['displayname'] = "liveblog"
    vf.vmx["memsize"] = "1024"
    vf.vmx["numvcpus"] = "1"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.name = "liveblog"
    vb.memory = "1024"
    vb.cpus = 1
  end
end
