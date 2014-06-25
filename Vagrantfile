
Vagrant.configure("2") do |config|
      config.vm.provider "docker" do |master|
                master.image   = "boxupp/centos-puppet:v1.1"
                master.name    = "master"
                master.volumes << '/var/lib/docker'
                master.has_ssh = true
        end
      
        config.vm.hostname  = "www.booxup.com"
                config.ssh.username = "root"
                config.ssh.password = "root123"
        config.vm.synced_folder "./keys" , "/vagrant"
        config.vm.synced_folder "manifests", "/etc/puppetlabs/puppet/manifests"
        config.vm.synced_folder "modules", "/etc/puppetlabs/puppet/modules"
        
        config.vm.provision  "puppet" do |master|
                master.manifests_path = "manifests"
                master.manifest_file = "site.pp"
                master.module_path = "modules"
        end
  end
                     
