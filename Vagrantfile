Vagrant.configure('2') do |config|
    config.vm.box = 'ubuntu/focal64'
    config.ssh.private_key_path =  ["~/.vagrant.d/insecure_private_key","./secrets/id_rsa"]
    config.disksize.size = '8GB'
    config.ssh.insert_key = false
    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 1
      end
    config.vm.disk :disk, size: "2GB", name: "extra_storage1"
    config.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("./secrets/id_rsa.pub").first.strip
        s.inline = <<-SHELL
          echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
          echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
        SHELL
      end
end