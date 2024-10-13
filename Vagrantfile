Vagrant.configure("2") do |config|
    # Use the RHEL 8 box from Vagrant Cloud
    config.vm.box = "rockylinux/9"
    config.vm.box_url = "https://app.vagrantup.com/rockylinux/boxes/9/versions/4.0.0/providers/libvirt/amd64/vagrant.box"
  
    # Set VM name and hostname
    config.vm.hostname = "rhel8"
    config.vm.provider "qemu" do |q|
      # Customize the amount of memory and CPUs
      q.memory = "4096"
      q.cpus = 2
    end
  
    # Provisioning with Ansible
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "podman.yml"
    end
  end
  