#more info about configuration here is:
#https://github.com/vagrant-libvirt/vagrant-libvirt

Vagrant.configure("2") do |config|
 
  config.vm.define :am do |am|
    am.vm.box = "debian/stretch64"
    am.vm.hostname = "master"
    am.vm.network  "private_network", ip: "192.168.121.9"
           am.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/playbook.yaml"
              end
    am.vm.provision "shell", inline: <<-SHELL
      #install ANSIBLE
      su
      echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list
      apt-get install dirmngr --install-recommends -y
      apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 
      apt-get update
      apt-get install ansible -y

     # sudo   sed -i '/\[defaults\]/a    inventory     = /etc/ansible/mount-folder/hosts.yml' /etc/ansible/ansible.cfg 

      apt-get install tree -y 

    SHELL
    am.vm.synced_folder "./ansible", "/etc/ansible/mount-folder"
    am.vm.provider "libvirt" do  |libvirt, override|
      libvirt.cpus = 4
      #libvirt.storage :file, :size => '20G'
      libvirt.memory = "2048"
      libvirt.default_prefix = "vagrantVM"
      end
  end

  #   config.vm.define :client01 do |client01|
  #   client01.vm.box = "debian/stretch64"
  #   client01.vm.hostname = "client01"
  #   client01.vm.network  "private_network", ip: "192.168.121.10"
  # end

  #   config.vm.define :client02 do |client02|
  #   client02.vm.box = "debian/stretch64"
  #   client02.vm.hostname = "client02"
  #   client02.vm.network  "private_network", ip: "192.168.121.11"
  # end

   #onfig.vm.synced_folder "/home/GAMELOFT/valera.pelenskyi/VagrantProject/vm01/vm01_data_share", "/var/www"

   (1..2).each do |i|
    config.vm.define "client#{i}" do |client|
      client.vm.box = "debian/stretch64"
      client.vm.hostname = "client0#{i}"
      client.vm.network  "private_network", ip: "192.168.121.1#{i}"
      client.vm.provider "libvirt" do  |libvirt, override|
        libvirt.cpus = 2
        #libvirt.storage :file, :size => '20G'
        libvirt.memory = "1024"
        libvirt.default_prefix = "vagrantVM"
      end
     end
    end
    
end