VAGRANT_API_VERSION = "2"
Vagrant.configure(VAGRANT_API_VERSION) do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.hostname = "5GCvm"
  config.vm.network "private_network", ip:"192.168.56.101" 
  config.vm.synced_folder "open5gs_config" , "/etc/open5gs/"
  config.vm.synced_folder "data" , "/home/vagrant/data"
  config.vm.network "forwarded_port", guest: 80, host: 8086


  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    vb.cpus = 2
    vb.memory = "4096"
  end
  
  config.vm.provision "shell", inline: <<-SHELL

     apt-get -y update
     apt-get install -y gnupg wget tcpdump 
     wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc > key.asc 
     sudo apt-key add key.asc
     echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
     apt-get -y update
     ap-get install -y mongodb-org
     sudo systemctl start mongod
     sudo systemctl enable mongod
     add-apt-repository ppa:open5gs/latest
     apt-get install -y software-properties-common
     apt-get -y update
     apt-get install -y open5gs
     #sudo apt install libc6=2.31-0ubuntu9.2 libc-bin=2.31-0ubuntu9.2 - To be used if getting error for nodejs
     
    #  curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o  /usr/share/keyrings/nodesource.gpg
    #  echo "deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_20.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
    #  sudo apt-get -y update 
    #  sudo apt-get -y install nodejs
    #  mkdir -p /usr/lib/node_modules/open5gs
    #  sudo curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -
    #  sudo cp /home/vagrant/data/open5gs_webui.service /lib/systemd/system/open5gs-webui.service
    #  sudo systemctl daemon-reload
    #  sudo systemctl restart open5gs-webui
     



  SHELL


end
