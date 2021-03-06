# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # set to false, if you do NOT want to check the correct VirtualBox Guest Additions version when booting this box
  if defined?(VagrantVbguest::Middleware)
    config.vbguest.auto_update = true
  end

  config.vm.box = "ubuntu/trusty64"
  config.vm.network :forwarded_port, guest: 5601, host: 1234
  config.vm.network :forwarded_port, guest: 9200, host: 9209
  config.vm.network :forwarded_port, guest: 9300, host: 9309
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "2", "--memory", "4096"]
  end

  config.vm.provider "vmware_fusion" do |v, override|
     ## the puppetlabs ubuntu 14-04 image might work on vmware, not tested? 
    v.box = "phusion/ubuntu-14.04-amd64"
    v.vmx["numvcpus"] = "2"
    v.vmx["memsize"] = "4096"
  end
  config.vm.provision :shell,
    :keep_color => true,
    :path => "setup.sh"
end
