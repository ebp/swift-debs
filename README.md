Swift Distribution
==================

This repo contains built .deb packages for Ubuntu 14.04 x64.


Installation
------------
```sh
# Fetch this repo
git clone git://github.com/ebp/swift-debs.git /usr/local/src/swift-debs
cd /usr/local/src/swift-debs

# Add to apt sources
echo 'deb file:/usr/local/src/swift-debs ./' | sudo tee -a /etc/apt/sources.list

# Update apt and install
sudo apt-get update
sudo apt-get install swift python-swift
# Any other specific packages, depending on server type
sudo apt-get install swift-account swift-container swift-object swift-object-expirer swift-proxy
```

Building
--------
*NOTE: These instructions use v2.2.2 as an example.*

Install development requirements for .deb and Swift:
```sh
# Swift dependencies
sudo apt-get install dpkg-dev devscripts debhelper \
  python-all-dev python-mock python-nose python-sphinx python-oslosphinx

# Additional python-swiftclient dependencies
sudo apt-get install python-coverage python-concurrent.futures python-fixtures \
  python-subunit python-testtools testrepository
```

Fetch the appropriate \*.orig.tar.gz, \*.debian.tar.xz, and \*.dsc from
https://launchpad.net/ubuntu/+source/swift and
https://launchpad.net/ubuntu/+source/python-swiftclient
```sh
# For example:
wget https://launchpad.net/ubuntu/+archive/primary/+files/swift_2.2.2.orig.tar.gz
wget https://launchpad.net/ubuntu/+archive/primary/+files/swift_2.2.2-0ubuntu1.debian.tar.xz
wget https://launchpad.net/ubuntu/+archive/primary/+files/swift_2.2.2-0ubuntu1.dsc
wget https://launchpad.net/ubuntu/+archive/primary/+files/python-swiftclient_2.3.1.orig.tar.gz
wget https://launchpad.net/ubuntu/+archive/primary/+files/python-swiftclient_2.3.1-0ubuntu1.debian.tar.xz
wget https://launchpad.net/ubuntu/+archive/primary/+files/python-swiftclient_2.3.1-0ubuntu1.dsc
```

Unpack the source and apply patches:
```sh
dpkg-source -x swift_2.2.2-0ubuntu1.dsc
dpkg-source -x python-swiftclient_2.3.1-0ubuntu1.dsc
```

This will create a `swift-2.2.2` directory.
Generate `.deb` files (as a non-root user):
```sh
cd swift-2.2.2
debuild -us -uc -b
cd python-swiftclient-2.3.1
debuild -us -uc -b
```

To update, remove the existing files in `debs` and replace them with newly-generated
packages, then regenerate the `Packages` file:
```sh
./update-packages.sh
```
