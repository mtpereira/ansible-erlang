# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

boxes = {
  "ubuntu-trusty"  => {
                        :name => "ubuntu-trusty",
                        :box => "boxcutter/ubuntu1404",
                        :ip => '10.0.0.52',
                        :cpu => "100",
                        :ram => "128"
                      },
  "debian-jessie"  => {
                        :name => "debian-jessie",
                        :box => "boxcutter/debian8",
                        :ip => '10.0.0.53',
                        :cpu => "100",
                        :ram => "128"
                      },
}

File.open('./inventory','w') do |f|
  boxes.each { |key, value| f.puts("#{key} ansible_ssh_host=#{value[:ip]} ansible_ssh_user=vagrant\n") }
end

Vagrant.configure("2") do |config|
  boxes.each do |name, box|
    config.vm.define name do |machine|
      machine.vm.box = box[:box]
      machine.vm.box_url = box[:url]
      machine.vm.hostname = "%s" % box[:name]

      machine.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      machine.vm.network :private_network, ip: box[:ip]

      machine.vm.provision :ansible do |ansible|
        ansible.playbook = "test.yml"
        ansible.inventory_path = "./inventory"
        ansible.tags = ENV['ANSIBLE_TAGS'] ||= "all"
        ansible.verbose = ENV['ANSIBLE_VERBOSE'] ||= "vvvv"
      end
    end
  end
end

