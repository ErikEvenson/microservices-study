# -*- mode: ruby -*-
# vi: set ft=ruby :

# Configuration settings
VAGRANT_VERSION_REQUIRE = ">= 1.7.4"
VAGRANTFILE_API_VERSION = "2"

# Lock down vagrant version.
Vagrant.require_version VAGRANT_VERSION_REQUIRE

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  if Vagrant.has_plugin?("vagrant-cachier")
    # Configure cached packages to be shared between instances of the same base box.
    # More info on the "Usage" link above
    config.cache.scope = :box
  end

  # Tells vagrant to build the image based on the Dockerfile found in
  # the same directory as this Vagrantfile.
  config.vm.define "microservice-a" do |container|
    container.vm.provider "docker" do |docker|
      docker.name = "web"
      docker.build_dir = "."
      docker.ports = ['8888:8888']
      docker.remains_running = true
      docker.vagrant_vagrantfile = "./Vagrantfile.proxy"
    end
  end

  config.vm.network :forwarded_port, host: 8888, guest: 8888
end
