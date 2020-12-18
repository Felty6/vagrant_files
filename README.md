#Operating Vagrant (Document)

Create a folder to operate vagrant
mkdir vagrant_getting_started

In that folder, activate the vagrant
vagrant init

By now, it has provided you with "Vagrantfile" and
now, you need to choose your vagrant box:

Vagrant.configure("2") do |config|
config.vm.box = "centos/8"
config.vm.box_version = "1905.1"

###Configuring the Network###
config.vm.network :forwarded_port, guest: 80, host: 8080

Now, you can try to boot up the environment and type:
vagrant up
vagrant ssh

#Install a Webserver

Create a directory where Apache will check your files
mkdir html
touch index.html

(As an example)
~index.html~
<!DOCTYPE html>
<html>
  <body>
    <h1>Getting started with Vagrant!</h1>
  </body>
</html>

Shell script to set up Apache

(As an example)
~bootstrap.sh~
#!/usr/bin/env bash
yum update
yum install -y httpd
if ! [ -L /var/www ]; then
  rm -rf /var/www
  ln -fs /vagrant /var/www
fi

#Provisioning the Webserver
vagrant reload --provision

#Enter the SSH
vagrant ssh

#Access the Web Page
http://127.0.0.1:8080
