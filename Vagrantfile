# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

require 'ipaddr'
Vagrant.configure("2") do |config|

  # config.vm.box = "ubuntu/artful64"
  config.vm.box = "ubuntu/trusty64"

  first_private_ip =  "192.168.33.33"

  nodes = {
    'node1' => { 
      'node_id' => 1,
      'ip' => "192.168.33.33",
      'zoo_host_port' => 8080,
      'kafka_host_port' => 8180

    },
#     'node2' => { 
#       'node_id' => 2,
#       'ip' => "192.168.33.34",
#       'zoo_host_port' => 8081,
#       'kafka_host_port' => 8181
#     },
#     'node3' => { 
#       'node_id' => 3,
#       'ip' => "192.168.33.35",
#       'zoo_host_port' => 8082,
#       'kafka_host_port' => 8182
#     }
  }

  brokers = Array.new 
  nodes.each do |name, info|
    brokers.push(info['ip'])
  end
  nodes.each_with_index do |(name, info), index|
    puts "Node#{info['node_id']}"

    # config.vm.define "node#{index}" do |node|
    config.vm.define "node#{info['node_id']}" do |node|
      node.vm.hostname=name
      node.vm.network "private_network", ip: info['ip']
      # node.vm.provision :shell, path: "bootstrap.sh", :args => "#{id} #{info['ip']} #{brokersStr} "

      node.vm.provision :ansible do |ansible|

        # Disable default limit to connect to all the machines
        ansible.limit = "all"
        ansible.playbook = "ansible/playbook.yml"
        ansible.extra_vars = {
          index: index,
          node_id: info['node_id'],
          ip: info['ip'],
          brokers: brokers
        }
      end

      node.vm.network "forwarded_port", guest: 2181, host: info['zoo_host_port']
      node.vm.network "forwarded_port", guest: 9092, host: info['kafka_host_port']   
      node.vm.provider "virtualbox" do |vb|
        # Display the VirtualBox GUI when booting the machine
        vb.gui = false
      
        # Customize the amount of memory on the VM:
        vb.memory = "2048"
      end
    end  
  end

end
