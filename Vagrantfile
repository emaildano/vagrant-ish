Vagrant.require_version '>= 1.6.0'
VAGRANTFILE_API_VERSION = '2'
require 'yml'

servers = YAML.load_file('server.yml')

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "server.yml"
  end

end
