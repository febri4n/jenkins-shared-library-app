Vagrant.configure("2") do |master|
  master.vm.box = "ubuntu/jammy64"

  master.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4098"
    vb.cpus = 4
    vb.linked_clone = true
  end

  master.vm.define "jenkins-vm" do |jenkins|
    jenkins.vm.network :private_network, ip: "192.168.1.12"
  end

end

Vagrant.configure("2") do |slave|
  slave.vm.box = "ubuntu/jammy64"

  slave.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
    vb.linked_clone = true
  end

  slave.vm.define "jenkins-vm-agent" do |agent|
    agent.vm.network :private_network, ip: "192.168.1.13"
  end

end
