# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 8084
  config.vm.network :private_network, ip: "192.168.58.111"

  config.vm.provider :virtualbox do |vb|
    vb.customize [
          "setextradata", :id,
      "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant-root", "1"
    ]

    vb.customize [
      'modifyvm', :id,
      '--natdnshostresolver1', 'on',
      '--memory', '512',
      '--cpus', '1'
    ]
  end
  config.vm.provision :ansible do |ansible|
        ansible.limit = "all"
        ansible.playbook = "go_app.yml"
      end
end
