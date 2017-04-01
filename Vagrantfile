
$num_instances = 1
$ins_memory = 1024

Vagrant.configure("2") do |config|
	(1..$num_instances).each do |i|
		config.vm.define "node#{i}" do |node|
		# 设置虚拟机的Box
		node.vm.box = "CentOS7.1"
		# 设置虚拟机的主机名
		node.vm.hostname="node#{i}"
		# 设置虚拟机的IP
		node.vm.network "private_network", ip: "192.168.59.#{i+200}"
		# 设置主机与虚拟机的共享目录
		node.vm.synced_folder "./data", "/home/vagrant/data"
		# VirtaulBox相关配置
		node.vm.provider "virtualbox" do |v|
			# 设置虚拟机的名称
			v.name = "node#{i}"
			# 设置虚拟机的内存大小  
			v.memory = 1024
			# 设置虚拟机的CPU个数
			v.cpus = 1
		end
  
		# 使用shell脚本进行软件安装和配置
		node.vm.provision "shell", inline: <<-SHELL
			# 安装docker 1.11.0
			#wget -qO- https://get.docker.com/ | sed 's/docker-engine/docker-engine=1.11.0-0~trusty/' | sh
			#usermod -aG docker vagrant
			yum install vim net-tools -y 
			systemctl restart network.service
			
		SHELL
		end
	end
end