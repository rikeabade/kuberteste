# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {

  'kube-master'   => {'memory' => '2048', 'cpus' => 2, 'ip' => '101', 'box' => 'ubuntu/focal64', 'provision' => 'kube-master.sh'},
  'kube-worker-1' => {'memory' => '2048', 'cpus' => 2, 'ip' => '102', 'box' => 'ubuntu/focal64', 'provision' => 'kube-master.sh'},
  'kuber-worker-2'=> {'memory' => '2048', 'cpus' => 2, 'ip' => '103', 'box' => 'ubuntu/focal64', 'provision' => 'kube-master.sh'},
  'postgresql'    => {'memory' => '2048', 'cpus' => 2, 'ip' => '104', 'box' => 'ubuntu/focal64', 'provision' => 'kube-master.sg'},
}

Vagrant.configure('2') do |config|

  config.vm.box_check_update = false

  vms.each do |name, conf|
    config.vm.define "#{name}" do |my|
      my.vm.box = conf['box']
      my.vm.hostname = "#{name}.example.com"
      my.vm.network 'private_network', ip: "172.16.100.#{conf['ip']}"
      my.vm.provision 'shell', path: "provision/#{conf['provision']}"
      my.vm.provider 'virtualbox' do |vb|
        vb.memory = conf['memory']
        vb.cpus = conf['cpus']
      end
      my.vm.provider 'libvirt' do |lv|
        lv.memory = conf['memory']
        lv.cpus = conf['cpus']
        lv.cputopology :sockets => 1, :cores => conf['cpus'], :threads => '1'
      end
    end
  end
end
