Vagrant.configure("2") do |config|

 # creating a virtual machine ubuntu 
 config.vm.box = "ubuntu/xenial64"
 # create a private network with provided ip address
 config.vm.network "private_network", ip: "192.168.10.100"
 
 # Synced app folder
 config.vm.synced_folder ".", "/home/vagrant/app"

 # Provisioning
 config.trigger.after :up, :provision do |trigger|
    config.vm.provision "shell", path: "provision.sh"
 end
 


end
