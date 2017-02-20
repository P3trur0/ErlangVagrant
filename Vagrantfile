# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
HOSTNAME_MACHINE = 'erlangbox'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.box = "ubuntu/trusty64"
	

  	hostname = HOSTNAME_MACHINE
  

	# Shared folders
	config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant"

	# Removes "stdin: is not a tty" annoyance as per
	# https://github.com/SocialGeeks/vagrant-openstack/commit/d3ea0695e64ea2e905a67c1b7e12d794a1a29b97
	config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

	#setup X-Forwarding
	config.ssh.forward_x11 = true

	config.vm.provider "virtualbox" do |vb|
		vb.customize	[
					"modifyvm", :id,
					"--memory", 1024,
				]  

  	config.vm.provision "shell", inline: <<-shell
  	  wget http://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
  	  sudo dpkg -i erlang-solutions_1.0_all.deb

  	  wget http://packages.erlang-solutions.com/debian/erlang_solutions.asc
  	  sudo apt-key add erlang_solutions.asc
	
	    apt-get update
	    apt-get install erlang -y --force-yes
  	shell
	end
end

