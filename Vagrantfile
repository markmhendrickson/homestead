# Switching to nfs for only those who want it
# thanks http://www.jedi.be/blog/2011/03/28/using-vagrant-as-a-team/
# http://vagrantup.com/docs/nfs.html
use_nfs = false #RUBY_PLATFORM.include?('darwin')
# http://www.ruby-forum.com/topic/86488
# mac: puts RUBY_PLATFORM => i686-darwin10
# windows: puts RUBY_PLATFORM => i386-mingw32

# the path to the code that will be used...
use_path = "/vagrant"

Vagrant::Config.run do |config|

  config.vm.box = "lucid64"
  config.vm.box_url = "http://files.vagrantup.com/lucid64.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  share_folder_flags = {}
  if(use_nfs)
  
    # Assign this VM to a host only network IP, allowing you to access it
    # via the IP.
    config.vm.network "33.33.33.11"
  
    share_folder_flags = {:nfs => true}
  
  end

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  # config.vm.forward_port "http", 80, 8080
  config.vm.forward_port "web", 80, 8084
  #config.vm.forward_port "gearman", 4730, 4730

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  config.vm.share_folder "v-data", use_path, "./", share_folder_flags

  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "cookbooks"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  config.vm.provision :chef_solo do |chef|
  
    #chef.cookbooks_path = [File.join("config","cookbooks"), File.join("config","site-cookbooks")]
    chef.cookbooks_path = File.join("config","cookbooks")
    
    chef.add_recipe("apache2")
    chef.add_recipe("apache2_config")
    #chef.add_recipe("apt")
    
  end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_server do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # IF you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end
