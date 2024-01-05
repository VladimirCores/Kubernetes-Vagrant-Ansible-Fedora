Vagrant.configure("2") do |config|
  config.vm.box = "generic/fedora39"

  VM_CPUS = 1
  VM_MEMORY = 2048
  
  config.vagrant.plugins = "vagrant-libvirt"

  config.ssh.insert_key = false
  
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :libvirt do |libvirt|
    libvirt.memory = VM_MEMORY
    libvirt.cpus = VM_CPUS
    libvirt.qemu_use_session = false
    libvirt.username = "root"
    libvirt.password = "password"
  end

  config.vm.define "control-plane" do |cp|
    cp.vm.hostname = "controlplane.k8s.local"
    cp.vm.network :private_network, ip: "192.168.60.4"
    cp.vm.provision :ansible do |ansible|
      # disable default limit to connect to all the machines
      # execute playbook1 on all hosts
      ansible.limit = "all"
      ansible.playbook = "playbook-control-plane.yaml"
      ansible.compatibility_mode = "2.0"
    end
  end

  # config.vm.define "worker-1" do |app|
  #   app.vm.hostname = "worker1.k8s.local"
  #   app.vm.network :private_network, ip: "192.168.60.5"
  # end

  # config.vm.define "worker-2" do |app|
  #   app.vm.hostname = "worker2.k8s.local"
  #   app.vm.network :private_network, ip: "192.168.60.6"
  # end
end
