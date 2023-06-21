# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
	config.vm.define "inetRouter", primary: true do |inetRouter|
		inetRouter.vm.box = "centos/7"
		inetRouter.vm.hostname = "inetRouter"
		inetRouter.ssh.insert_key = false
		inetRouter.vm.provider "virtualbox" do |vb|
				vb.memory = "512"
				vb.cpus = "1"
			end
		inetRouter.vm.network "private_network",
			ip: "192.25.10.10",
			virtualbox__intnet: true,
			name: "routerNet"
		inetRouter.vm.provision "ansible", run: "always", type: "ansible_local"  do |ansible|
			ansible.become = true
			ansible.playbook = "/vagrant/playbooks/inetRouter.yml"
		end
	end	
	
	config.vm.define "inetRouter2", primary: true do |inetRouter2|
		inetRouter2.vm.box = "centos/7"
		inetRouter2.vm.hostname = "inetRouter2"
		inetRouter2.vm.provider "virtualbox" do |vb|
				vb.memory = "512"
				vb.cpus = "1"
			end
		inetRouter2.vm.network "private_network",
			ip: "192.168.34.11"
		inetRouter2.vm.network "forwarded_port", 
			guest: 80, 
			host: 8080,
			auto_correct: true,
			guest_ip: "192.168.34.11"
		inetRouter2.vm.network "private_network",
			ip: "192.25.10.12",
			virtualbox__intnet: true,
			name: "routerNet"
		inetRouter2.vm.provision "ansible", run: "always", type: "ansible_local"  do |ansible|
			ansible.become = true
			ansible.playbook = "/vagrant/playbooks/inetRouter2.yml"
		end
	end	
	
	config.vm.define "centralRouter", primary: true do |centralRouter|
		centralRouter.vm.box = "centos/7"
		centralRouter.vm.hostname = "centralRouter"
		centralRouter.vm.provider "virtualbox" do |vb|
				vb.memory = "512"
				vb.cpus = "1"
			end
		centralRouter.vm.network "private_network", 
			ip: "192.25.10.11",
			virtualbox__intnet: true,
			name: "routerNet"
		centralRouter.vm.network "private_network", 
			ip: "192.168.12.10",
			virtualbox__intnet: true,
			name: "officeNet"	
		centralRouter.vm.provision "ansible", run: "always", type: "ansible_local"  do |ansible|
			ansible.become = true
			ansible.playbook = "/vagrant/playbooks/centralRouter.yml"
		end			
	end	
	
	config.vm.define "centralServer", primary: true do |centralServer|
		centralServer.vm.box = "centos/7"
		centralServer.vm.hostname = "centralServer"
		centralServer.vm.provider "virtualbox" do |vb|
				vb.memory = "512"
				vb.cpus = "1"
			end
		centralServer.vm.network "private_network",
			ip: "192.168.12.11",
			virtualbox__intnet: true,
			name: "officeNet"
		centralServer.vm.provision "ansible", run: "always", type: "ansible_local"  do |ansible|
			ansible.become = true
			ansible.playbook = "/vagrant/playbooks/centralServer.yml"
		end
				
	end	

end
