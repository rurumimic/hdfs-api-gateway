# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.define vm_name = "zimmer" do |config|
    config.vm.hostname = "zimmer"
    config.vm.network :private_network, ip: "192.168.10.101"
    config.vm.network "forwarded_port", guest: 8000, host: 8000
    config.vm.provision "docker"
    config.vm.provision "file", source: "./zimmer/kong", destination: "kong"
    config.vm.provision "shell", inline: <<-SHELL
      curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose
      sudo curl -L https://raw.githubusercontent.com/docker/compose/1.26.2/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
    SHELL
  end

  config.vm.define vm_name = "amadeus" do |config|
      config.vm.hostname = "amadeus"
      config.vm.network :private_network, ip: "192.168.20.101"
      config.vm.network "forwarded_port", guest: 50070, host: 50070
      config.vm.network "forwarded_port", guest: 50075, host: 50075
      config.vm.provider :virtualbox do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end

      config.vm.provision "file", source: "./data/hadoop-2.10.0.tar.gz", destination: "hadoop-2.10.0.tar.gz"
      config.vm.provision "shell", inline: <<-SHELL
        yum install -y java-1.8.0-openjdk-devel
        echo 'export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk/jre' >> /home/vagrant/.bash_profile

        ssh-keygen -t rsa -P '' -f /home/vagrant/.ssh/id_rsa
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
        chmod 0600 /home/vagrant/.ssh/authorized_keys
        
        tar -zxf /home/vagrant/hadoop-2.10.0.tar.gz
        mv /home/vagrant/hadoop-2.10.0 /home/vagrant/hadoop

        echo 'export HADOOP_HOME=/home/vagrant/hadoop' >> /home/vagrant/.bash_profile
        echo 'export PATH=$PATH:$HADOOP_HOME/bin' >> /home/vagrant/.bash_profile
        echo 'export PATH=$PATH:$HADOOP_HOME/sbin' >> /home/vagrant/.bash_profile

        chown -R vagrant:vagrant /home/vagrant
      SHELL
  end

  config.vm.define vm_name = "bach" do |config|
    config.vm.hostname = "bach"
    config.vm.network :private_network, ip: "192.168.30.101"
    config.vm.network "forwarded_port", guest: 50071, host: 50071
    config.vm.network "forwarded_port", guest: 50076, host: 50076
    config.vm.provider :virtualbox do |vb|
        vb.memory = 2048
        vb.cpus = 1
    end

    config.vm.provision "file", source: "./data/hadoop-2.10.0.tar.gz", destination: "hadoop-2.10.0.tar.gz"
      config.vm.provision "shell", inline: <<-SHELL
        yum install -y java-1.8.0-openjdk-devel
        echo 'export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk/jre' >> /home/vagrant/.bash_profile

        ssh-keygen -t rsa -P '' -f /home/vagrant/.ssh/id_rsa
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
        chmod 0600 /home/vagrant/.ssh/authorized_keys
        
        tar -zxf /home/vagrant/hadoop-2.10.0.tar.gz
        mv /home/vagrant/hadoop-2.10.0 /home/vagrant/hadoop

        echo 'export HADOOP_HOME=/home/vagrant/hadoop' >> /home/vagrant/.bash_profile
        echo 'export PATH=$PATH:$HADOOP_HOME/bin' >> /home/vagrant/.bash_profile
        echo 'export PATH=$PATH:$HADOOP_HOME/sbin' >> /home/vagrant/.bash_profile

        chown -R vagrant:vagrant /home/vagrant
      SHELL
  end
  
end
