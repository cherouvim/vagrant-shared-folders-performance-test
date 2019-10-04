Vagrant.configure(2) do |config|

  config.vm.box = "geerlingguy/ubuntu1804"
  config.vm.box_version = "1.1.1"
  config.vm.box_check_update = false
  config.ssh.password = "vagrant"
  
  # Needed for NFS share.
  # Windows users make sure you've run: vagrant plugin install vagrant-winnfsd.
  config.vm.network "private_network", type: "dhcp"
  
  # /app0 is inside vm without sharing
  config.vm.synced_folder "app1", "/app1", type: "nfs"
  config.vm.synced_folder "app2", "/app2"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
    vb.name = "_vagrant-2019"
    vb.linked_clone = true
    vb.customize ['modifyvm', :id, '--audio', 'none']
  end
  
  config.vm.provision "shell", inline: <<-SHELL

    which nodejs || curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
    which nodejs || apt-get install nodejs

    mkdir -p /app0

    rm -rf /app?/*

    echo "\n************* app0 *************"
    cd /app0
    cp /vagrant/package* .
    ls -al .
    echo "**** npm installing..."
    time npm install
    echo "**** doing some sed..."
    time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1
    
    echo "\n************* app1 *************"
    cd /app1
    cp /vagrant/package* .
    ls -al .
    echo "**** npm installing..."
    time npm install
    echo "**** doing some sed..."
    time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1
    
    echo "\n************* app2 *************"
    cd /app2
    cp /vagrant/package* .
    ls -al .
    echo "**** npm installing..."
    time npm install
    echo "**** doing some sed..."
    time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1
    
  SHELL

end
