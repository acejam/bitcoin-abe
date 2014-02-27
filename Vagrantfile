Vagrant.configure("2") do |config|
  
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 9332, host: 9320
 #config.vm.synced_folder "data/", "/srv"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "docker" do |d|
  end

  config.vm.provision "shell", inline: "apt-get -y install mysql-client"
  config.vm.provision "shell", inline: "docker build -t mysql /vagrant/."
  config.vm.provision "shell", inline: "docker run -d -p 3306:3306 -v /data/mysql:/var/lib/mysql mysql"

end