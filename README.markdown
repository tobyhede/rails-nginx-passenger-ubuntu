AMI
------------

* [Ubuntu-32-10.10](http://aws.amazon.com/amis/4349)
* [Ubuntu-64-10.10](http://aws.amazon.com/amis/4350)


Basics
------------

### Install core libs

* apt-get update
* apt-get install -y build-essential zlib1g-dev libssl-dev openssl libcurl4-openssl-dev libreadline6-dev libmysqlclient15-dev git

### Configure SSH

* nano /etc/ssh/sshd_config

    ---
      Port 4242
      Protocol 2
      PermitRootLogin no
      PasswordAuthentication no
      UseDNS no
      AllowUsers ubuntu deploy



### Configure iptables

* [iptables](https://gist.github.com/3365ce0aa5b1bcd694a0)

       sudo nano /etc/iptables.up.rules
       sudo /sbin/iptables-restore < /etc/iptables.up.rules
       sudo nano /etc/network/if-pre-up.d/iptables
        #!/bin/sh
        /sbin/iptables-restore < /etc/iptables.up.rules        
     



Ruby on Rails
------------

### Install rvm:

* bash < <( curl http://rvm.beginrescueend.com/releases/rvm-install-head )
* Add rvm config to ~/.bashrc


### Install Ruby 1.9.2 & Bundler

* rvm install 1.9.2
* gem install bundler
* edit ~/.gemrc

    ---
      :sources:
        - http://gems.rubyforge.org
        - http://gems.github.com
      gem: --no-ri --no-rdoc



### Install & Configure nginx

* gem install passenger
* download and untar the nginx src
* rvmsudo passenger-install-nginx-module:

      # select option 2
      # give it the path to the nginx src
      # add this option when prompted:
     --with-http_gzip_static_module

* Add [nginx config](https://gist.github.com/16e8143b5d0a849b58cb) to /opt/nginx/conf/nginx.conf

      server {
        listen 80;
        #server_name www.yourhost.com;
        root /u/Glaive/current/public;                                       
        passenger_enabled on;
      }

* [nginx init script](https://github.com/tobyhede/rails-nginx-passenger-ubuntu/raw/master/nginx/nginxt)

      git clone git://github.com/tobyhede/rails-nginx-passenger-ubuntu.git
      sudo mv rails-nginx-passenger-ubuntu/nginx/nginx /etc/init.d/nginx
      sudo chown root:root /etc/init.d/nginx
    
      sudo /etc/init.d/nginx start
      sudo /etc/init.d/nginx status
      sudo /usr/sbin/update-rc.d -f nginx defaults
    

Analysis
------------

* mpstat 

      sudo apt-get install sysstat
      sudo mpstat



References
-----------
[Maverick Ubuntu Setup](http://articles.slicehost.com/2010/10/18/ubuntu-maverick-setup-part-1)







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

