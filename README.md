# vagrant-shared-folders-performance-test

## Environment setup (windows)

1. Install latest VirtualBox from https://www.virtualbox.org/wiki/Downloads
2. Install latest VirtualBox Extension Pack from https://www.virtualbox.org/wiki/Downloads
3. Install latest vagrant from https://www.vagrantup.com/downloads.html
4. Run `vagrant plugin install vagrant-winnfsd`
5. Run `vagrant up` to bring the VM up. First "up" will provision VM.
6. Run `vagrant provision` to test the speed.
7. Run `vagrant destroy --force` to remove VM.

## Environment setup (ubuntu)

1. Install latest virtualbox from https://www.virtualbox.org/wiki/Downloads \
   or an older version using `sudo apt-get install virtualbox`
2. Install latest VirtualBox Extension Pack from https://www.virtualbox.org/wiki/Downloads
3. Install latest vagrant from https://www.vagrantup.com/downloads.html \
   or an older version using `sudo apt-get install vagrant`
4. Install NFS `sudo apt-get install nfs-common nfs-kernel-server`.
5. Run `vagrant up` to bring the VM up. First "up" will provision VM.
6. Run `vagrant provision` to test the speed.
7. Run `vagrant destroy --force` to remove VM.
