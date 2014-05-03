!SLIDE new-chapter center

# Installation

!SLIDE

# Download VirtualBox

[http://www.virtualbox.org](http://www.virtualbox.org)

!SLIDE

# Install Vagrant
    $ (sudo) gem install vagrant


!SLIDE

# Add a basebox

    $ vagrant box add basebox \
      http://files.vagrantup.com/lucid64.box

!SLIDE

# Basebox = Mother of all VMs

!SLIDE

# Each Virtual Machine <br/>is based on a basebox


!SLIDE

# Initialize workspace

    $ cd ~/workspace
    $ vagrant init basebox


!SLIDE

# Customize Vagrantfile
    @@@ruby
    $ cat ./Vagrantfile
    Vagrant::Config.run do |config|
      config.vm.box = "basebox"
      config.vm.network "192.168.56.10"
      config.vm.forward_port "http", 3000, 3000
      config.vm.share_folder "v-data", "/data", "../data"
    end


!SLIDE

# Start up a Virtual Machine
    @@@ruby
    vagrant up

.notes Share code with rsync or shared folders
.notes vagrant ssh connects through NAT to the VM


!SLIDE

# Log in
    @@@ruby
    vagrant ssh


!SLIDE

# et voilá!
You got your VirtualMachine up and running!


!SLIDE

# Deploy code eg. with Capistrano
     @@@bash
     cap deploy

!SLIDE

# or shared folders
    @@@ruby
    $ cat ./Vagrantfile
    Vagrant::Config.run do |config|
      config.vm.share_folder "v-data", "/data", "../data"
    end

!SLIDE

# Use port forwarding
    @@@ruby
    $ cat ./Vagrantfile
    Vagrant::Config.run do |config|
      config.vm.forward_port "http", 3000, 3000
    end

!SLIDE

# Or enter a static IP

    @@@ruby
    $ cat ./Vagrantfile
    Vagrant::Config.run do |config|
      config.vm.network "192.168.56.10"
    end


!SLIDE new-chapter center

# Next steps


!SLIDE

# Customize VMs
eg. with Chef cookbooks
    @@@ruby
    $ cat ./Vagrantfile
    …
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "rails"
      chef.add_role "web"
    end


!SLIDE

# Run Chef on the VM
    $ vagrant provision

.notes This runs chef-solo

!SLIDE

# Share a VM with colleagues
    @@@ruby
    $ vagrant box repackage mybasebox


!SLIDE

# Create your <br/>*own* baseboxes
    @@@ruby
    $ gem install veewee
    $ vagrant basebox define \
      'mybasebox' \
      'ubuntu-10.10-server-i386'


!SLIDE

# Share / search baseboxes
[http://vagrantbox.es](http://vagrantbox.es)

!SLIDE

# Excellent documentation
[http://vagrantup.com/docs/](http://vagrantup.com/docs/)
