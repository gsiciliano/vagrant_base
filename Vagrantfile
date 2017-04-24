# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

VAGRANTFILE_API_VERSION = "2"

required_plugins = %w(vagrant-hostmanager)

# Installs required plugins and restarts vagrant
required_plugins.each do |plugin|
  need_restart = false
  unless Vagrant.has_plugin? plugin
    system "vagrant plugin install #{plugin}"
    need_restart = true
  end
  exec "vagrant #{ARGV.join(' ')}" if need_restart
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define 'localtest.machine' do |machine|
    machine.vm.box = "ubuntu/trusty64"
    machine.vm.network "private_network", ip: "172.16.16.16"
    machine.hostmanager.aliases = ["webserver.local"]
    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.verbose  = true
      ansible.limit    = "all"
      ansible.tags     = "provision-app"
      ansible.sudo = true
    end
  end

end
