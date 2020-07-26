# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
 "elasticstack" => {"memory" => "2048", "cpu" => "2", "ip" => "1", "image" => "centos/7"},
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.synced_folder ".", "/vagrant", disabled: true
      machine.ssh.forward_agent = true
      machine.vm.network "private_network", ip: "192.168.33.#{conf["ip"]}"
      machine.vm.network "forwarded_port", guest: 5601, host: 8080, protocol: "tcp"
      machine.vm.hostname = "#{name}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
      end
    end
  end

end
