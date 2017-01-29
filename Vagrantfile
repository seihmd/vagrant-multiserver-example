# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    VAGRANT_VM_PROVIDER = "virtualbox"
    machineNames = ["example.com.web", "example.com.db"]
    config.vm.box = "centos/7"

    N = 1

    (0..N).each do |index|
        config.vm.define machineNames[index] do |machine|
            machine.vm.hostname = machineNames[index]
            machine.vm.network "forwarded_port", guest: 80, host: 10020 + index, guest_ip: "192.168.30.#{10+index}"
            machine.vm.network "private_network", ip: "192.168.30.#{10+index}",  virtualbox__intnet: "example.com"
            machine.vm.network "private_network", ip: "192.168.30.#{10+index}"

            if index == N
                machine.vm.provision :ansible do |ansible|
                    ansible.limit = "all"
                    ansible.playbook = "site.yml"
                    ansible.inventory_path = "staging"
                    # ansible.verbose = "-vvvv"
                end
            end
        end
    end
end