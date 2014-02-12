vagrant-rackspace-ansible
=========================

A collection of Vagrantfile's using the vagrant-rackspace plugin to bootstrap servers with test Ansible playbooks.

## Requirements

+ Vagrant 1.4.3+
+ vagrant-rackspace
+ Ansible 1.5+

For Vagrant, follow a normal install using their packaged binaries. Keep in mind that local gem installs of Vagrant is not supported and will break things as you upgrade or work with your environment.

  [http://www.vagrantup.com/downloads.html](http://www.vagrantup.com/downloads.html)

The same goes for Ansible, find a package for your distrobution, or for OS X homebrew works great. A pip install is not recommended unless you know what you are doing or are using a development build.

  [http://docs.ansible.com/intro_installation.html](http://docs.ansible.com/intro_installation.html)

The vagrant-rackspace Vagrant plugin is required with this project since the Vagrantfile is majorly geared towards using this. To install, just run:

    vagrant plugin install vagrant-rackspace

## Settings

For ease of use, a newly created vagrant-rackspace.rc file has been created to centralize the options for configuration. The Vagrantfile in each project requires for at least the following environmental variables to be set:

    OS_USERNAME=USERNAME
    OS_PASSWORD=API_KEY

Using SSH keys, we can seemlessly bootstrap a server and is recommended. This requires a bit of leg work on the Rackspace side, but is easy and a majority of the work is done for you. Using the Rackspace API, create a new keypair that can be injected into servers, and use a redirect to save the private key locally. If you have used OpenStack, the process is familiar. Using python-novaclient is a great way to do this:

    nova keypair-add NAME > id_rsa.pem

Information on setting up the python-novaclient for Rackspace can be seen here:

[http://www.rackspace.com/knowledge_center/article/installing-python-novaclient-on-linux-and-mac-os](http://www.rackspace.com/knowledge_center/article/installing-python-novaclient-on-linux-and-mac-os)

Now, you can export configuration for the public key to be used, and your local private key. Both options are included for your configuration in the vagrant-rackspace.rc file:

    RS_KEYPATH=/path/to/generated/id_rsa.pem
    RS_KEYNAME=NAME

You can also export the following optional environmental variables, again included in the vagrant-rackspace.rc file. This is also their defaults in the plugin if not set at all:

    RS_RACKCONNECT=false
    RS_REGION=ORD

Lastly, the default server is a 1GB Performance cloud server with Ubuntu 12.04. You are free to configure this with the following environmental variables:

    RS_FLAVOR=performance1-1
    RS_IMAGE=/Ubuntu 12.04/

## How to Use

Once you are done editing your vagrant-rackspace.rc file, source it and boot your Rackspace cloud servers as you would any Vagrant project. Vagrant will bootstrap your server with the Ansible playbooks as configured:

    source vagrant-rackspace.rc
    cd project_dir/
    vagrant up --provider=rackspace

It is recommended to view the README of each project directory for their specifics on how many servers will be booted, and what playbooks are used.
