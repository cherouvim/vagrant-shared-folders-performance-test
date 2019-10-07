Vagrant.configure(2) do |config|

  config.vm.box = "geerlingguy/ubuntu1804"
  config.vm.box_version = "1.1.1"
  config.vm.box_check_update = false
  config.ssh.password = "vagrant"

  # Needed for NFS share.
  config.vm.network "private_network", type: "dhcp"

  if Vagrant::Util::Platform.windows? then
    config.vagrant.plugins = ["vagrant-winnfsd"]
    config.vm.synced_folder "app1", "/app1", type: "nfs"
  else
    config.vagrant.plugins = ["vagrant-bindfs"]
    config.vm.synced_folder "app1", "/app1", type: "nfs"
    config.bindfs.bind_folder "/app1", "/app2"
    config.nfs.map_uid = Process.uid
    config.nfs.map_gid = Process.gid
  end

  config.vm.synced_folder "app3", "/app3"

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
    rm -rf /app?/*

    
    mkdir -p /app0
    chown vagrant:vagrant /app0

    echo "\n************* app0 *************"
    runuser -l vagrant -c "cd /app0; cp /vagrant/package* .; ls -al ."
    echo "**** npm installing..."
    runuser -l vagrant -c "cd /app0; time npm install"
    echo "**** doing some sed..."
    runuser -l vagrant -c "cd /app0; time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1; rm -rf *"
    
    echo "\n************* app1 *************"
    runuser -l vagrant -c "cd /app1; cp /vagrant/package* .; ls -al ."
    echo "**** npm installing..."
    runuser -l vagrant -c "cd /app1; time npm install"
    echo "**** doing some sed..."
    runuser -l vagrant -c "cd /app1; time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1; rm -rf *"
    
    echo "\n************* app2 *************"
    runuser -l vagrant -c "cd /app2; cp /vagrant/package* .; ls -al ."
    echo "**** npm installing..."
    runuser -l vagrant -c "cd /app2; time npm install"
    echo "**** doing some sed..."
    runuser -l vagrant -c "cd /app2; time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1; rm -rf *"
    
    echo "\n************* app3 *************"
    runuser -l vagrant -c "cd /app3; cp /vagrant/package* .; ls -al ."
    echo "**** npm installing..."
    runuser -l vagrant -c "cd /app3; time npm install"
    echo "**** doing some sed..."
    runuser -l vagrant -c "cd /app3; time grep -rl variable . | xargs sed -i 's/variable/xxx/g' 2>&1; rm -rf *"
    
  SHELL

end
