# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_IP = "192.168.33.11"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/opt/superdesk", 
    :nfs => true,
    :mount_options => ['actimeo=2']
  config.vm.network :private_network, ip: VAGRANT_IP

  # Grunt server + Vagrant
  # https://coderwall.com/p/cyi5iq/grunt-server-vagrant-port-forwarding-ips
  config.vm.network "forwarded_port", guest: 9000, host:9000
  config.vm.network "forwarded_port", guest: 35729, host: 35729

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
    vf.vmx["memsize"] = "2048"
    vf.vmx["numvcpus"] = "1"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.name = "liveblog"
    vb.memory = "2048"
    vb.cpus = 1
  end
end
