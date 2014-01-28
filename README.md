# My chef cookbooks

I'm using these cookbooks with my [vagrantfiles](https://github.com/chrisekelley/vagrant-couchdb).

Includes recipes for apt, build-essential, couchdb, erlang, and squid.

## Squid

The squid recipe has been customised a little bit.

Had to reconfigure the squid.conf, the first line was incorrect:

    # <= "acl all src" if node['squid']['version'].to_i <3 >
    acl all src all

This is in the squid.conf.erb template file in the cookbook.

Command for updating squid settings whenever you change its config:

    sudo squid -N -k reconfigure


If you want to prevent a domain from being cache, add the following to squid.conf:

    acl cnn dstdomain www.cnn.com
    cache deny cnn

## Installing new cookbooks

    gem install chef
    knife cookbook site download build-essential

## Building your own cookbooks

I used the [installing-couchdb-virtualbox](http://architects.dzone.com/articles/installing-couchdb-virtualbox) guide.

I modified the recipe to use the source recipe for couchdb so that couch 1.5 would be installed.

    mkdir vagrant-cookbooks
    cd vagrant-cookbooks
    git clone https://github.com/opscode-cookbooks/apt
    git clone https://github.com/opscode-cookbooks/erlang.git
    git clone https://github.com/opscode-cookbooks/couchdb.git
    cd ..
    mkdir vagrant-couchdb
    cd vagrant-couchdb
    vagrant init
