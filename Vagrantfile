# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network "forwarded_port", guest: 15443, host: 15443

  # Add in some memory improvements (be nice to ourselves)
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  # Update apt-get once
  $update_apt_get = <<SCRIPT
  if ! test -f .updated_apt_get; then
    sudo apt-get update
    touch .updated_apt_get
  fi
SCRIPT
  config.vm.provision "shell", inline: $update_apt_get

  # Install latest stable version of `node` and `npm`
  # https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#ubuntu-mint-elementary-os
  $install_node = <<SCRIPT
  if ! which node &> /dev/null; then
    sudo apt-get install -y python-software-properties python g++ make
    sudo add-apt-repository -y ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install -y nodejs
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_node

  # Install dependency on `git`
  $install_git = <<SCRIPT
  if ! which git &> /dev/null; then
    sudo apt-get install git -y
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_git

  # Install dependency on elasticsearch (and Java)
  # https://gist.github.com/wingdspur/2026107
  $install_elasticsearch = <<SCRIPT
  if ! which java &> /dev/null; then
    sudo apt-get install openjdk-7-jre-headless -y
  fi

  # TODO: Figure out how to add to /usr/local/bin
  # if ! which elasticsearch &> /dev/null; then
  #   cd /tmp
  #   wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.1.0.deb
  #   sudo dpkg -i elasticsearch-1.1.0.deb
  #   # TODO: Is this necessary?
  #   # sudo service elasticsearch start
  # fi
SCRIPT
  config.vm.provision "shell", inline: $install_elasticsearch

  # Install dependency on CouchDB
  # https://launchpad.net/~couchdb/+archive/stable
  $install_couchdb = <<SCRIPT
  if ! which couchdb &> /dev/null; then
    sudo apt-get install python-software-properties -y
    sudo add-apt-repository ppa:couchdb/stable -y
    sudo apt-get update
    sudo apt-get install couchdb -y
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_couchdb

  # Install dependency on Redis
  $install_redis = <<SCRIPT
  if ! which redis-server &> /dev/null; then
    sudo apt-get install redis-server -y
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_redis

  # Clone `npm-www` repository
  $clone_repository = <<SCRIPT
  cd /vagrant
  if ! test -d npm-www &> /dev/null; then
    git clone https://github.com/npm/npm-www.git
  fi
SCRIPT
  config.vm.provision "shell", inline: $clone_repository

  # Notify the user of next steps
  $notify_user = <<SCRIPT
  echo "\`npm-www\` is ready to go"
  echo "To start the app, inside of \`vagrant ssh\`, run the following:"
  echo "cd /vagrant/npm-www"
  echo "npm run dev"
  echo ""
  echo "On your host machine, you can access \`npm-www\` at:"
  echo "https://127.0.0.1:15443/"
SCRIPT
  config.vm.provision "shell", inline: $notify_user
end
