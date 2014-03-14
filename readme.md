PostGIS box
===========
Using Vagrant + Ansible to set up a virtual linux machine running
PostgreSQL 9.1 with PostGIS 2.0 (should have had 9.3 / 2.1, but that
repo doesn't seem to play well with ansible).


Installation (Ubuntu)
---------------------
The installation of following software will be described under:

* [VirtualBox](http://virtualbox.org/)
* [Vagrant](http://www.vagrantup.com/)
* [Ansible](http://www.ansibleworks.com/)

1. Install VirtualBox:

    `apt-get install -y virtualbox`

    Use the VirtualBox installer from http://virtualbox.org/ if the version in
    apt is older than 4.x (verify with
    `apt-cache show virtualbox | grep 'Version:'`).

2. Install the Vagrant package for Ubuntu from the
[Vagrant download page](http://www.vagrantup.com/downloads.html).

    The Vagrant version available in apt is (usually) outdated.

3. Install Ansible using pip:

    `pip install ansible`

    The Ansible version available in apt is (usually) outdated.

4. Install NFS package (required for folder sharing between host and guest):

    `apt-get install -y nfs-kernel-server`

5. OPTIONAL: Install the vagrant plugin which upgrades the vb guest addonsbis when necessary
   `vagrant plugin install vagrant-vbguest`

6. Create the Vagrant dev VM:

    `vagrant up`

    This will download the base Vagrant box, configure a VM and provision it
    using Ansible. The provision step automatically configures required
    databases.

Adding databases
----------------
See provisioning/playbook.yml, under vars, databases you can add more. Run

    vagrant provision

to add more..


Operation
---------

From your host machine you can connect to a db like so:

    PGUSER=username PGPASSWORD=password psql -h localhost -d database_name -p 15432

Or, to get full access, ssh into the vagrant box:

    vagrant ssh
    sudo su - postgres
    psql

To start the virtualmachine:

    vagrant up

To stop it:

    vagrant halt
