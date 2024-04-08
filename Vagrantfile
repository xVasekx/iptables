MACHINES = {
  :inetRouter => {
        :vm_name => "inetRouter",
        #:public => {:ip => "10.10.10.1", :adapter => 1},
        :net => [   
                    #ip, adpter, netmask, virtualbox__intnet
                    {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"}, 
                    {ip: '192.168.56.10', adapter: 8},
                ]
  },

  :centralRouter => {
        :vm_name => "centralRouter",
        :net => [
                   {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.57.1', adapter: 3, netmask: "255.255.255.0", virtualbox__intnet: "dir-net"},
		   {ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "router-net2"},
                   {ip: '192.168.56.11', adapter: 8},
                ]
  },

  :centralServer => {
        :vm_name => "centralServer",
        :net => [
          {ip: '192.168.57.2', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "dir-net"},
                   {ip: '192.168.56.12', adapter: 8},
                ]
  },

  :inet2Router => {
        :vm_name => "inet2Router",
        :net => [
                   {ip: '192.168.255.10', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "router-net2"},
                   {ip: '192.168.56.15', adapter: 8},
                ]
  },

}

ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
#      box.vm.box = "generic/ubuntu2204"
      box.vm.box = "ubuntu/jammy64"
      box.vm.host_name = boxconfig[:vm_name]
      
      box.vm.provider "virtualbox" do |v|
        v.memory = 512
        v.cpus = 1
       end

      boxconfig[:net].each do |ipconf|
        box.vm.network "private_network", **ipconf
      end

      box.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh
      SHELL
    end
  end
end
