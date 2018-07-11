
Vagrant.configure("2") do |config|
 
  config.vm.define :amaster do |amaster|
    amaster.vm.box = "debian/stretch64"
    amaster.vm.hostname = "master"
    amaster.vm.network  "private_network", ip: "192.168.121.9"
           amaster.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/playbook.yaml"
              end
    amaster.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install tree
    SHELL
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
      client.vm.hostname = "client#{i}"
      client.vm.network  "private_network", ip: "192.168.121.1#{i}"

      # client.vm.provider "libvirt" do |vb|
      #   vb.name = "client#{i}"
      #   vb.cpus = 2
      #   vb.memory = "1024"
      # end
     end
    end
    
end