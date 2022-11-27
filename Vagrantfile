# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "ip" => "30", "image" => "bento/ubuntu-18.04"},
  "worker01" => {"memory" => "1024", "cpu" => "1", "ip" => "31", "image" => "bento/ubuntu-18.04"},
  "worker02" => {"memory" => "1024", "cpu" => "1", "ip" => "32", "image" => "bento/ubuntu-18.04"},
  "worker03" => {"memory" => "1024", "cpu" => "1", "ip" => "33", "image" => "bento/ubuntu-18.04"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "public_network", ip: "192.168.10.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        
      end
      machine.vm.provision "shell", path: "script.sh"
      
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end

    end
  end
end
