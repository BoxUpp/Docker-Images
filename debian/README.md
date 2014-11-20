#Docker

This is docker file for instaling ssh service and puppet on Debian Image.  

#Puppet Provisioning in docker container through Vagrant.

This is a sample vagrant file for puppet provisioning in Debian container through Vagrant.

```Vagrantfile
Vagrant.configure("2") do |config|
                config.vm.provider "docker" do |master|
                master.image   = "‎boxupp/debian-base:latest"
                master.name    = "master"
                master.volumes << '/var/lib/docker'
                master.has_ssh = true
        end
        config.vm.hostname  = "www.booxup.com"
                config.ssh.username = "root"
                config.ssh.password = "root123"
           
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
