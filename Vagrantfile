Vagrant.configure("2") do |config|

  config.vm.box = "centos-6.4-32"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.memory = 1024
  end

  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.network :forwarded_port, guest: 389, host: 1389
  config.vm.network :forwarded_port, guest: 10389, host: 10389
  config.vm.network :forwarded_port, guest: 8080, host: 8080

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "fortress-in-a-box.yml"
    ansible.groups = {
	"fortress" => ["default"]
    }
    #ansible.raw_arguments = ['-v','-M ./modules']
  end

end
