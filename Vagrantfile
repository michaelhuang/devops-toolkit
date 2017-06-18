# -*- mode: ruby -*-
# vi: set ft=ruby :
$repo_script = <<SCRIPT

sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup
wget -O /etc/apt/sources.list http://mirrors.aliyun.com/repo/ubuntu1404-lts.list
sudo apt-get clean
sudo apt-get update

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end
  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 2048
  end
  config.vm.define :dev do |dev|
    dev.vm.network "private_network", ip: "10.100.199.200"
    dev.vm.provision :shell, :inline => $repo_script
    dev.vm.provision :shell, path: "bootstrap.sh"
    dev.vm.provision :shell,
      inline: 'PYTHONUNBUFFERED=1 ansible-playbook \
        /vagrant/ansible/dev.yml -c local'
  end
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
    config.vbguest.no_install = true
    config.vbguest.no_remote = true
  end
end
