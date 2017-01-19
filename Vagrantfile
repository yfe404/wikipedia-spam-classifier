# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Install Docker
  config.vm.provision :shell, path: "bootstrap.sh"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8888" will access port 8888 on the guest machine.
  config.vm.network "forwarded_port", guest: 8888, host: 8888

  # Build the image revscoring Docker image 
  # More info at https://github.com/wiki-ai/revscoring
  config.vm.provision "docker" do |d|
    d.build_image "/vagrant/revscoring",
    args: "--rm -t nealmcb/revscoring:latest"
  end

  # Run Iptyhon within the image
  # web-based interface at http://localhost:8888/
  # share the folder /vagrant/notebooks (within the VM) with 
  # the folder /notebooks within the container 
  config.vm.provision "docker" do |d|
    d.run "nealmcb/revscoring",
    args: "-p 8888:8888 -v /vagrant/notebooks/:/notebooks",
    cmd: "jupyter notebook --no-browser"
  end

end
