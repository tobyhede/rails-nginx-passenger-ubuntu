AMI
------------
Ubuntu-32-10.10: http://aws.amazon.com/amis/4349


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
* rvmsudo passenger-install-nginx-module
* Add nginx config to /opt/nginx/conf/nginx.conf

      server {
      listen 80;
      #server_name www.yourhost.com;
      root /u/Glaive/current/public;                                       
      passenger_enabled on;
      }

* [nginx init script](git@github.com:tobyhede/rails-nginx-passenger-ubuntu.git)

      git clone git://github.com/jnstq/rails-nginx-passenger-ubuntu.git
      sudo mv rails-nginx-passenger-ubuntu/nginx/nginx /etc/init.d/nginx
      sudo chown root:root /etc/init.d/nginx
    
      sudo /etc/init.d/nginx start
      sudo /etc/init.d/nginx status
      sudo /usr/sbin/update-rc.d -f nginx defaults
    
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

