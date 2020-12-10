Vagrant.configure("2") do |config|

  config.vm.define "web_server_1" do |web_server_1|
    web_server_1.vm.box = "ubuntu/trusty64"
    web_server_1.vm.hostname = 'webserver1'
    web_server_1.vm.box_url = "ubuntu/trusty64"

    web_server_1.vm.network :private_network, ip: "192.168.56.101"

  end

  config.vm.define "web_server_2" do |web_server_2|
    web_server_2.vm.box = "ubuntu/trusty64"
    web_server_2.vm.hostname = 'webserver2'
    web_server_2.vm.box_url = "ubuntu/trusty64"

    web_server_2.vm.network :private_network, ip: "192.168.56.102"


  end

    config.vm.define "loadbalancer" do |loadbalancer|
    loadbalancer.vm.box = "ubuntu/trusty64"
    loadbalancer.vm.hostname = 'loadbalancer'
    loadbalancer.vm.box_url = "ubuntu/trusty64"

    loadbalancer.vm.network :private_network, ip: "192.168.56.103"


  end

    config.vm.define "master" do |master|
    master.vm.box = "ubuntu/trusty64"
    master.vm.hostname = 'master'
    master.vm.box_url = "ubuntu/trusty64"

    master.vm.network :private_network, ip: "192.168.56.100"
    master.vm.provision "file", source: "web-server-playbook.yml", destination: "$HOME/"
    master.vm.provision "file", source: "loadbalancer-playbook.yml", destination: "$HOME/"
    master.vm.provision "file", source: "haproxy.cfg", destination: "$HOME/"
    master.vm.provision "file", source: "haproxy_sticky_session.cfg", destination: "$HOME/"
    master.vm.provision "file", source: "inventory", destination: "$HOME/"
    master.vm.provision "file", source: "static_site.cfg", destination: "$HOME/ansible-files/static_site.cfg"
    # master.vm.provision "file", source: "static-site-src/", destination:"$HOME/ansible-files/"
    

    master.vm.provision "shell", inline: <<-SHELL
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt update
    yes Y | sudo apt install ansible
    SHELL
  end
end