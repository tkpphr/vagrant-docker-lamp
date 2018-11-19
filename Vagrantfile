Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder "./docker", "/vagrant/docker"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
    v.cpus = 2
    v.memory = 2048
  end
  config.vm.provision :docker, run: "always"
  config.vm.provision :docker_compose,
    yml: "/vagrant/docker/docker-compose.yml",
    compose_version: "1.21.2",
    run: "always"
end
