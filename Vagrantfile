# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-16.04"

  config.vm.network :forwarded_port, guest: 9200, host: 9201, host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 5601, host: 5602, host_ip: "127.0.0.1"

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "4096"
  end

  config.vm.provision "shell", inline: <<-END
  sudo apt-get update
  sudo apt-get install -y default-jdk
  sudo apt-get install unzip
END

  config.vm.provision "shell", privileged: false, path: 'es_install.sh'

  config.vm.provision "shell", privileged: false, path: 'kibana_install.sh'

  config.vm.provision "shell", inline: <<-END
  cp /vagrant/elasticsearch.service /etc/systemd/system/elasticsearch.service
  cp /vagrant/kibana.service /etc/systemd/system/kibana.service
  systemctl daemon-reload
  systemctl enable elasticsearch
  systemctl start elasticsearch
  systemctl start kibana
END

end
