Vagrant.configure("2") do |config|
    config.vm.box = "rockylinux/9"

    config.vm.hostname = "rocky9"
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.cpus = 2
    end

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "podman.yml"
    end
  end
  