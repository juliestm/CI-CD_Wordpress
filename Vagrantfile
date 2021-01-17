$app_ip = "172.17.17.100"
$mysql_ip = "172.17.18.100"
$monitoring_ip = "172.17.19.100"

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.box_check_update = false

    # Ansible provisioning
    config.vm.provision "ansible" do |ansible|
	ansible.playbook = "provision/main.yml"
	ansible.extra_vars = {
	    app_ip: $app_ip,
	    mysql_ip: $mysql_ip,
	    monitoring_ip: $monitoring_ip
	}
    end

    # Конфигурация машины БД mysql
    config.vm.define "mysql" do |mysql|
	mysql.vm.network "private_network", ip: $mysql_ip
	mysql.vm.hostname = "mysql"

	mysql.vm.provider "virtualbox" do |vb|
	    vb.memory = "1024"
	end
    end

    # Конфигурация машины приложения (nginx+php+wordpress)
    config.vm.define "app" do |app|
	app.vm.network "private_network", ip: $app_ip
	app.vm.hostname = "app"

	app.vm.network  "forwarded_port", guest: 80, host: 8888

	app.vm.provider "virtualbox" do |vb|
	    vb.memory = "1024"
	end
    end

    # Конфигурация машины мониторинга
    config.vm.define "monitoring" do |monitoring|
	monitoring.vm.network "private_network", ip: $monitoring_ip
	monitoring.vm.hostname = "monitoring"

	monitoring.vm.network  "forwarded_port", guest: 3000, host: 3333
	monitoring.vm.network  "forwarded_port", guest: 9090, host: 9999

	monitoring.vm.provider "virtualbox" do |vb|
	    vb.memory = "1024"
	end
    end
end