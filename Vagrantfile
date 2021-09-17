Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.box = "debian/buster64"
  config.vm.box_check_update = false

  config.vm.define "host1" do |host|
    host.vm.hostname = "host1"
    host.vm.network "private_network", ip: "192.168.99.50"
    host.vm.provider "virtualbox" do |vb|
      vb.name = "host1"
      vb.memory = "512"
      vb.cpus = 1
    end
  end

  config.vm.define "host2" do |host|
    host.vm.hostname = "host2"
    host.vm.network "private_network", ip: "192.168.99.60"
    host.vm.provider "virtualbox" do |vb|
      vb.name = "host2"
      vb.memory = "512"
      vb.cpus = 1
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.groups = {
      "servers"     => ["host[1:2]"],
      "web-servers" => ["host1"],
      "block-icmp"  => ["host2"]
    }
    ansible.verbose = true
  end
end
