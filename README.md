# Setting up the Puma Daemon Service

This repo includes modified scripts found from a [technpol](https://technpol.wordpress.com/2014/04/16/configuring-puma-init-d-scripts-and-pumactl-on-debian-with-rvm/) post that help with setting up a Puma Daemon Service.

## Installation

    # Copy the init script to the services directory
    sudo cp install/puma /etc/init.d/puma
    sudo chmod 755 /etc/init.d/puma

    # Make it start at boot time
    sudo update-rc.d -f puma defaults
    
    # Copy the Puma runner
    sudo cp install/run-puma* /usr/local/bin
    sudo chmod 755 /usr/local/bin/run-puma*
    
    # Create an empty configuration file
    sudo touch /etc/puma.conf

You can either update the puma apps to run by editing the /etc/puma.conf and adding a line for each app. The structure of the line is as follows:

    app-path,user,config-file-path,log-file-path

Or you can add an instance by running the following command:

    sudo /etc/init.d/puma add /path/to/app user /path/to/app/config/puma.rb /path/to/app/config/log/puma.log

## Configuring Service Directory

In order to use an app with the Puma Daemon Service, your directory must be setup with the following folder structure:

    /dir/to/app
    |~config/
    | |+puma.rb
    |~log/
    |~tmp/
    | |+pids/

You can copy the example config file located in the /config directory of this repo into your folder. All you should have to do is change the base path at the top to your application folder to get started.

## Start and stop services

Now that you have everthing setup, you can run the following commands to start and stop services.

    # Start all puma services
    /etc/init.d/puma start
    
    # Stop all puma services
    /etc/init.d/puma stop
