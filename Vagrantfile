IMAGE_NAME = "ubuntu/focal64"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
    end
	
	



  config.vm.define "web" do |web|
        web.vm.box = IMAGE_NAME
        web.vm.network "private_network", ip: "192.168.2.21"
        web.vm.hostname = "web"
        web.vm.provision :shell, inline: "apt update && apt -y  purge python2.7-minimal && apt install -qy ansible"
        web.vm.provision "ansible_local" do |ansible|
            ansible.version = "2.9.6"
            ansible.playbook = "setup/web-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.2.21",
                
            }
        end
    end	
	
	
    config.vm.define "jenkins" do |jenkins|
        jenkins.vm.box = IMAGE_NAME
        jenkins.vm.network "private_network", ip: "192.168.2.10"
        jenkins.vm.network :forwarded_port, guest: 8080, host: 8080, auto_correct: true
        jenkins.vm.hostname = "jenkins"
        jenkins.vm.provision :shell, inline: "apt update && apt -y  purge python2.7-minimal && apt install -qy ansible"
        jenkins.vm.provision "file", source: "./setup/docker", destination: "$HOME/dockerfiles"
        jenkins.vm.provision "ansible_local" do |ansible|
            ansible.version="2.9.6"
            ansible.playbook = "setup/jenkins-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.2.10"
            }
        end
      jenkins.vm.provision :shell, inline: "cd /home/vagrant/dockerfiles/; ./up.sh"
    end

end