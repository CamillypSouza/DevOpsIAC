# -- mode: ruby --
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Configuração da VM
  config.vm.box = "generic/debian12"

  # Nome da VM
  config.vm.hostname = "p01-camilly"

  # Configuração de rede
  config.vm.network "private_network", ip: "192.168.57.55"

  # Configuração do provider VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.name = "p01-camilly" # Nome da VM no VirtualBox
    vb.memory = "1024"      # Memória RAM
    vb.cpus = 2             # CPUs
  end

  # Adicionar 3 discos adicionais de 10 GB
  config.vm.disk :disk, size: "10GB", name: "disk1"
  config.vm.disk :disk, size: "10GB", name: "disk2"
  config.vm.disk :disk, size: "10GB", name: "disk3"

  # Configurar Ansible para provisionamento automático
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "/playbooks/main_playbook.yml"
    
  end
end
