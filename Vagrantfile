$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server"
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "mysqldb" do |mysql|
    mysql.vm.network "public_network", ip: "192.168.1.25"

    mysql.vm.provision "shell", inline: $script_mysql
    mysql.vm.provision "shell", inline: "service mysql restart"
    mysql.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "phpweb" do |phpweb|
    phpweb.vm.network "forwarded_port", guest: 80, host: 8089
    phpweb.vm.network "public_network", ip: "192.168.1.26"
  end
end
