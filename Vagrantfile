Vagrant.configure("2") do |config|

  config.vm.box = "centos-6.4-32"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.network :forwarded_port, guest: 389, host: 10389
  config.vm.network :forwarded_port, guest: 8080, host: 18080

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "fortress-in-a-box.yml"
    ansible.inventory_path = "ansible_inventory.ini"
    ansible.extra_vars = {
      fortress_version: "1.0-RC39"
    }
#    ansible.tags = [
#      "commander"
#    ]
    ansible.skip_tags = [
      "regression_commander",
      "regression_fortress"
    ]
  end

end