# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/trusty64'

  # Fix for: "stdin: is not a tty"
  # https://github.com/mitchellh/vagrant/issues/1673#issuecomment-28288042
  config.ssh.shell = %{bash -c 'BASH_ENV=/etc/profile exec bash'}

  config.vm.hostname = 'server'

  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision :shell, :inline => 'sudo apt-get update'

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'deploy.yml'
    ansible.groups = {
      'sentry' => ['default']
    }
    ansible.sudo = true
  end
end
