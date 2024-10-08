Vagrant.configure("2") do |config|
    # Указываем ОС, версию, количество ядер и ОЗУ
    config.vm.box = "rockylinux/9"
 
    config.vm.provider :virtualbox do |v|
      v.memory = 3072
      v.cpus = 2
    end
  
    # Указываем имена хостов и их IP-адреса
    boxes = [
      { :name => "ipa.otus.lan",
        :ip => "192.168.57.10",
      },
      { :name => "client1.otus.lan",
        :ip => "192.168.57.11",
      },
      { :name => "client2.otus.lan",
        :ip => "192.168.57.12",
      }
    ]
    # Цикл запуска виртуальных машин
    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.ssh.insert_key = false
        config.vm.hostname = opts[:name]
        config.vm.network "private_network", ip: opts[:ip]

        if opts[:name] == "client2.otus.lan"
          config.vm.provision "ansible" do |ansible|
           ansible.playbook = "ansible/ldap.yml"
           #ansible.verbose = "vvv"
           ansible.limit = "all"
          end
    end
       end
    end
  end
