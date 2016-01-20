# -*- mode: ruby -*-
# # vi: set ft=ruby :

require "yaml"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Box
  config.vm.box = "ubuntu/trusty64"

  # Networking
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.50.4"

  # Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "launch-pad/server.yml"
  end

  # Hosts
  # config.hostsupdater.aliases = ["example.dev"]


  ANSIBLE_PATH = __dir__
  config_file = File.join(ANSIBLE_PATH, 'launch-pad/group_vars', 'all', 'main.yml')

  if File.exists?(config_file)
    wordpress_sites = YAML.load_file(config_file)['wordpress_sites']
    fail_with_message "No sites found in #{config_file}." if wordpress_sites.to_h.empty?
  else
    fail_with_message "#{config_file} was not found. Please set `ANSIBLE_PATH` in your Vagrantfile."
  end

  hostname, *aliases = wordpress_sites.flat_map { |(_name, site)| site['site_hosts'] }
  config.vm.hostname = hostname
  www_aliases = ["www.#{hostname}"] + aliases.map { |host| "www.#{host}" }

  if Vagrant.has_plugin? 'vagrant-hostsupdater'
    config.hostsupdater.aliases = aliases + www_aliases
  else
    fail_with_message "vagrant-hostsupdater missing, please install the plugin with this command:\nvagrant plugin install vagrant-hostsupdater"
  end

end
