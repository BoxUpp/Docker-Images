#Docker

This is docker file for instaling ssh service and puppet on Linux Centos Container.  

#Puppet Provisioning in docker container through Vagrantfile 

This is a sample vagrant file for puppet provisioning in linux container through vagrant-docker plugin.

```Vagrantfile
Vagrant.configure("2") do |config|
                config.vm.provider "docker" do |master|
                master.image   = "boxupp/centos-puppet:V1.0"
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
```


This a sample site.pp file for puppet provisoning.

```site
        node "www.booxup.com"
        {
               
               #Add your puppet modules 
               include jboss
        }



        if versioncmp($::puppetversion,'3.6.1') >= 0 {

        $allow_virtual_packages = hiera('allow_virtual_packages',false)

        Package {
                allow_virtual => $allow_virtual_packages,
                }
        }
```



###Contributors

The list of contributors can be found at: [https://github.com/BoxUpp/Puppet-Modules/graphs](https://github.com/BoxUpp/Puppet-Modules/graphs)

##Sites
####site :[http://paxcel.net/](http://paxcel.net/) 
####site :[http://boxupp.com/](http://boxupp.com/)
