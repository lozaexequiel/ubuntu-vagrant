Vagrant.configure("2") do |config|
	config.vm.box = "generic-x64/ubuntu2204"

	config.vm.provider "hyperv" do |h|
	  h.memory = 2048
	  h.cpus = 1
	end

	config.vm.provider "virtualbox" do |vb|
	  vb.memory = 2048
	  vb.cpus = 1
	end
      
	config.vm.provision "shell", inline: <<-SHELL
	  export DEBIAN_FRONTEND=noninteractive
	  apt-get update
	  apt-get upgrade -y
	  apt-get install -y xrdp xfce4 xfce4-goodies firefox

	  # Enable and start xrdp service
	  systemctl enable xrdp
	  systemctl start xrdp

	  # Allow RDP through the firewall
	  ufw allow 3389/tcp

	  # Configure xrdp to use xfce
	  echo "xfce4-session" >~/.xsession
	  service xrdp restart    
	SHELL

      end