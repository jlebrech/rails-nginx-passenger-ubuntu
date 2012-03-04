rails-nginx-passenger-ubuntu
============================

My notes on setting up a simple production server with ubuntu, nginx, passenger and mysql for rails.

Aliases
-------

    echo "alias ll='ls -l'" >> ~/.bash_aliases
    
edit .bashrc and uncomment the loading of .bash_aliases

If you have trouble with PATH that changes when doing sudo, see http://stackoverflow.com/questions/257616/sudo-changes-path-why then add the following line to the same file

    echo "alias sudo='sudo env PATH=$PATH'" >> ~/.bash_aliases
    

Update and upgrade the system
-------------------------------

    sudo apt-get update
    sudo apt-get upgrade

Configure timezone
-------------------

    sudo dpkg-reconfigure tzdata
    sudo apt-get install ntp
    sudo ntpdate ntp.ubuntu.com # Update time
    
Verify that you have to correct date and time with

    date

Configure hostname
-------------------

    sudo hostname your-hostname

Add 127.0.0.1 your-hostname

    sudo vim /etc/hosts
    
Write your-hostname in 
    
    sudo vim /etc/hostname
    
Verify that hostname is set
    
    hostname

Install mysql
---------------

This should be installed before Ruby Enterprise Edition becouse that will install the mysql gem.

    sudo apt-get install mysql-server libmysqlclient15-dev

Install Rubygems
----------------
sudo apt-get install rubygems1.8


    
Gemrc
-------

Add the following lines to ~/.gemrc, this will speed up gem installation and prevent rdoc and ri from being generated, this is not nessesary in the production environment.

    ---
    :sources:
    - http://gems.rubyforge.org
    - http://gems.github.com
    gem: --no-ri --no-rdoc
    

Install Ruby 1.9.2
------------------
    rvm install 1.9.2
    rvm use 1.9.2 --default



Install Rails 3.2
-----------------
    sudo gem install rails


Installing git
----------------

    sudo apt-get install git-core

Installing Passenger + nginx
----------------------------
    sudo -s
    nginx=stable # use nginx=development for latest development version
    add-apt-repository ppa:nginx/$nginx
    apt-get update 
    apt-get install nginx
    exit
    
    sudo gem install passenger

    
Generate ssh key
---------------
    ssh-keygen

add `~/.ssh/id_dsa.pub` to your github keys

Git Clone your project
----------------------
   `git clone ...`
   

Config nginx
-----------

    sudo vim /etc/nginx/sites-enabled/gambino-admin
    
Add a new virtual host

    server {
        listen 80;
        # server_name www.mycook.com;
        root /home/joe/gambino-server/mail_ticket/public;
        passenger_enabled on;
    }
    
Restart nginx

    sudo /etc/init.d/nginx restart
    
        

