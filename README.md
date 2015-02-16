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
These packages were captured from build output of
https://launchpad.net/ubuntu/+source/swift

To update, remove the existing files in `debs` and replace them with new
packages, then regenerate the `Packages` file:
```sh
./update-packages.sh
```
