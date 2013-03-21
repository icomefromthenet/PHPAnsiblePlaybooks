Vagrant::Config.run do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  
  config.vm.define :gate do |config|
    # Every Vagrant virtual environment requires a box to build off of.

    config.vm.box = "precise32"
    config.vm.host_name = "gateway1.testing.com"
    
    # The url from where the 'config.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    # config.vm.box_url = "http://domain.com/path/to/above.box"
  
    # Boot with a GUI so you can see the screen. (Default is headless)
    #config.vm.boot_mode = :gui
  
    # Assign this VM to a host-only network IP, allowing you to access it
    # via the IP. Host-only networks can talk to the host machine as well as
    # any other machines on the same network, but cannot be accessed (through this
    # network interface) by any external networks.
    config.vm.network :hostonly, "192.168.1.2"
 
    # Forward a port from the guest to the host, which allows for outside
    # computers to access the VM, whereas host only networking does not.
    #config.vm.forward_port 80, 8080

    # Share an additional folder to the guest VM. The first argument is
    # an identifier, the second is the path on the guest to mount the
    # folder, and the third is the path on the host to the actual folder.
    #config.vm.share_folder("v-root", "/vagrant", ".", :nfs => true)

    # Provision with Assimble plugin
     config.vm.provision :ansible do |ansible|
      # point Vagrant at the location of your playbook you want to run
      ansible.playbook = "gateway.yml"
  
      # the Vagrant VM will be put in this host group change this should
      # match the host group in your playbook you want to test
      ansible.hosts = "gateway"
    end
  end

  
  config.vm.define :web do |web_config|
    web_config.vm.box = "precise32"
    web_config.vm.host_name = "web1.testing.com"
    web_config.vm.network :hostonly, "192.168.1.30"
    web_config.vm.forward_port 80, 8080
    web_config.vm.share_folder("v-root", "/vagrant", ".", :nfs => true)
    web_config.vm.provision :ansible do |ansible|
      ansible.playbook = "webserver.yml"
      ansible.hosts = "webserver"
    end
  end



  config.vm.define :devweb do |devweb_config|

    devweb_config.vm.box = "precise32"
    devweb_config.vm.host_name = "devweb1.testing.com"
    devweb_config.vm.network :hostonly, "192.168.1.2"
    devweb_config.vm.forward_port 80, 8080
    devweb_config.vm.share_folder("v-root", "/vagrant", "../", :nfs => false)
    devweb_config.vm.provision :ansible do |ansible|
      ansible.playbook = "devteir.yml"
      ansible.hosts = ["appserver","appdatabase","devserver"]
    end
  end


  config.vm.define :db do |db_config|
 
    db_config.vm.box = "precise32"
    db_config.vm.host_name = "db1.testing.com"
    db_config.vm.network :hostonly, "192.168.1.3"
    db_config.vm.forward_port 3306, 8306
    db_config.vm.provision :ansible do |ansible|
      ansible.playbook = "database.yml"
      ansible.hosts = "database"
    end
  end
end


