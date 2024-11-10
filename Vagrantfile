# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.define "nginx_machine" do |nginx_machine| 
    nginx_machine.vm.network "forwarded_port", guest: 80, host: 8085
    nginx_machine.vm.network "private_network", ip: "192.168.56.10"
    nginx_machine.vm.provision "shell", name: "nginx_installation", inline: <<-SHELL
      sudo apt -y update
      sudo apt -y install nginx
      sudo mkdir -p /var/www/nginx_page/html
      sudo chown -R www-data:www-data /var/www/nginx_page/html
      sudo cp -vr /vagrant/html/* /var/www/nginx_page/html
      sudo chmod -R 755 /var/www/nginx_page
      sudo systemctl restart nginx
      sudo cp -v /vagrant/nginx_provisions/nginx-page /etc/nginx/sites-available/
      sudo ln -s /etc/nginx/sites-available/nginx-page /etc/nginx/sites-enabled/
      sudo systemctl restart nginx
    SHELL
    #The last thing you need to do is to add the following line to the /etc/hosts file on your host machine:
    #192.168.56.10      nginx-page.org
    nginx_machine.vm.provision "shell", name: "ftp_provision", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install vsftpd
      mkdir /home/vagrant/ftp
      sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.key -out /etc/ssl/certs/vsftpd.crt
      cp -v /vagrant/nginx_provisions/vsftpd.conf /etc/vsftpd.conf
      sudo systemctl restart vsftpd
    SHELL
  end 


end