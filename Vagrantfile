#
# This file configures Vagrant to use the provision.yml ansible playbook to 
# provision a Fedora virtual machine.
#

Vagrant.configure(2) do |config|

	# The base box to build on. We use a Fedora 21 box because Fedora rulez.
	config.vm.box = "ubuntu/trusty64"

	# Disable automatic box update checking. Don't need to do this everyt time
	# we start a box - just run `vagrant box outdated` instead.
	config.vm.box_check_update = false

	config.vm.network "forwarded_port", guest: 80, host: 8080

	# Create a private network for the box so we can access it
	# config.vm.network "private_network", ip: "192.168.33.102", auto_config: false

	config.vm.network "private_network", ip: "192.168.33.22"


    # Share an additional folder to the guest VM. The first argument is the path on the host to the actual folder.
    # The second argument is the path on the guest to mount the folder. 
    config.vm.synced_folder "/var/www/v3.wellbeingzone.co.uk", "/var/www/", type: "rsync", rsync__exclude: "vendor/"


	# Configure VirtualBox specifically
	config.vm.provider "virtualbox" do |vb|
		vb.memory = "1024"
	end


	# Provision using ansible.
	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "provision.yml"
		ansible.extra_vars = {
			"application_environment" => "local"
		}
		ansible.sudo = true
	end
end