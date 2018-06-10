Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.provider "virtualbox" do |vb|
    #vb.gui = true
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
  end

  #Sync folder
  config.vm.synced_folder "application", "/var/www/application",
    create: true,
    owner: "vagrant",
    group: "vagrant"

  # Port-forwarding to localhost
  config.vm.network "forwarded_port", guest: 80, host: 8081
  config.vm.network "forwarded_port", guest: 443, host: 8443
  config.vm.network "private_network", ip: "192.168.20.20"

  #forward ssh agent for git and vagrant box
  config.ssh.forward_agent = true

  #Ansible
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.install_mode = "pip"
    ansible.verbose = true
  end
end
