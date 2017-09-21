# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
settings = YAML.load_file 'vagrant.yaml'

Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/zesty64' # 17.04
  config.vm.hostname = 'jekyll-dev-box'

  config.vm.network :forwarded_port, guest: 4000, host: 4000

  config.vm.provision :shell, path: 'bootstrap.sh', keep_color: true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder settings['host_blog_folder'], "/blog"

  config.vm.provider 'virtualbox' do |v|
    v.memory = 2048
    v.cpus = 2
  end
end
