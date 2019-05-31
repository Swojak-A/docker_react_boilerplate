# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.network "private_network", ip: "44.44.44.4"
  config.vm.provider "virtualbox" do |v|
        v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "xxxXXXxxx Starting instalation! xxxXXXxxx"

    sudo apt-get update

    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
    sudo apt-get install -y nodejs
    sudo npm i -g serve
    sudo npm i -g pm2

    # sudo apt-get update
    # curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
  	# sudo apt-get install -y nodejs
  	# sudo npm install pushstate-server -g --silent
  	# mkdir /vagrant/app
    
    sudo apt-get -y install nginx
    sudo rm /etc/nginx/sites-enabled/default
    sudo touch /etc/nginx/sites-available/nodejs_settings
    sudo ln -s /etc/nginx/sites-available/nodejs_settings /etc/nginx/sites-enabled/nodejs_settings
    sudo echo 'server {
            location / {
                    proxy_pass http://127.0.0.1:8080;
                    proxy_set_header Host $host;
                    proxy_set_header X-Real-IP $remote_addr;
            }
    }' >> /etc/nginx/sites-available/nodejs_settings
    sudo systemctl restart nginx
    
    echo "xxxXXXxxx Done installing your virtual machine! xxxXXXxxx"
  SHELL
end