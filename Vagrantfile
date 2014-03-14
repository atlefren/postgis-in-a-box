# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64-current"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network :forwarded_port, guest: 5432, host: 15432
  config.vm.network "private_network", ip: "172.16.10.11"

  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
    end
    config.vm.provision :ansible do |ansible|
      ansible.host_key_checking = false
      ansible.playbook = "provisioning/playbook.yml"
      ansible.inventory_path = "provisioning/hosts-vagrant"
      ansible.verbose = false
    end
end
