# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network "forwarded_port", guest: 15443, host: 15443

  # Update apt-get once
  $update_apt_get = <<SCRIPT
  if ! test -f .updated_apt_get; then
    sudo apt-get update
    touch .updated_apt_get
  fi
SCRIPT
  config.vm.provision "shell", inline: $update_apt_get

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

  # Install test dependency on `git`
  $install_git = <<SCRIPT
  if ! which git &> /dev/null; then
    sudo apt-get install git -y
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_git

  # Clone `npm-www repository
  $clone_repository = <<SCRIPT
  cd /vagrant
  if ! test -d npm-www &> /dev/null; then
    git clone https://github.com/npm/npm-www.git
    # TODO: Perform `npm install` and `npm start`
  fi
SCRIPT
  config.vm.provision "shell", inline: $clone_repository

  # Notes from before
  # ---------------------
  # ELASTIC SEARCH
  # TODO: This should be in /tmp or /usr/local/lib
  # http://stackoverflow.com/questions/10268583/how-to-automate-download-and-installation-of-java-jdk-on-linux
  # wget http://download.oracle.com/otn-pub/java/jdk/7/jre-7-linux-x64.tar.gz --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"
  # tar xvf jre-7-linux-x64.tar.gz
  # sudo cp jre1.7.0/ /usr/local/lib/ -r
  # sudo ln -s /usr/local/lib/jre1.7.0/bin/java /usr/bin/java

  # wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.7.tar.gz
  # tar xvzf elasticsearch-0.90.7.tar.gz
  # sudo cp elasticsearch-0.90.7/ /usr/local/lib/ -r
  # PATH="$PATH:/usr/local/lib/elasticsearch-0.90.7/bin"

  # COUCH DB
  # https://launchpad.net/~couchdb/+archive/stable
  # sudo apt-get install python-software-properties -y
  # sudo add-apt-repository ppa:couchdb/stable -y
  # sudo apt-get update -y
  # sudo apt-get remove couchdb couchdb-bin couchdb-common -yf
  # sudo apt-get install -V couchdb -y
  # sudo start couchdb

  # REDIS
  # sudo apt-get install redis-server -y

  # Start the machine
  # sudo npm run dev
end
