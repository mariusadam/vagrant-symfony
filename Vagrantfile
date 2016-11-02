Vagrant.configure("2") do |config|
    # Configure the box to use
    config.vm.box       = 'precise64'
    config.vm.box_url   = 'http://files.vagrantup.com/precise64.box'

    # Configure the network interfaces
    config.vm.network "private_network", ip: "192.168.33.10"

    # Configure shared folders
    config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", :nfs => true
    config.vm.synced_folder "..", "/var/www", id: "application",  :nfs => true

    # Configure VirtualBox environment
    config.vm.provider :virtualbox do |v|
        v.name = (0...8).map { (65 + rand(26)).chr }.join
        v.customize [ "modifyvm", :id, "--memory", 512 ]
    end

    # Provision the box
    config.vm.provision :ansible do |ansible|
        ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
        ansible.playbook = "ansible/site.yml"
    end
end
