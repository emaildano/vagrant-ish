# -*- mode: ruby -*-
# # vi: set ft=ruby :

require "yaml"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Box
  config.vm.box = "ubuntu/trusty64"

  # Networking
  config.vm.host_name = "localhost"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.50.4"

  # Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "launch-pad/server.yml"
  end

  # Hosts
  # config.hostsupdater.aliases = ["testing.dev", "example.dev"]

  # group_vars = YAML.load_file('launch-pad/group_vars/all/main.yml')
  # group_vars['wordpress_sites'].each do |site|
  #   site_name = site['site_name']
  #   config.hostsupdater.aliases.push(site_name)
  # end

end
