require 'berkshelf/vagrant'

VAGRANTFILE_API_VERSION = "2"
DEVELOPER_BOOTSTRAP_PATH = "./test/integration/"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |c|
  c.vm.box = "lampbox-ubuntu-12.04-vsdev"
  c.vm.box_url = "https://dl.dropbox.com/s/c249j11hfxpzeji/precise32_dev_recentupdates.box "                  
  c.vm.hostname = "precise32.vsdev"
  c.vm.network(:forwarded_port, {:guest=>80, :host=>8080})
  c.vm.network(:forwarded_port, {:guest=>3306, :host=>3316})
  c.vm.network(:forwarded_port, {:guest=>443, :host=>8443})
  c.vm.network(:forwarded_port, {:guest=>1080, :host=>1080})
  c.vm.synced_folder ".", "/vagrant", disabled: true
  c.vm.synced_folder "./public", "/vagrant/public", mount_options: ['dmode=777','fmode=666']
  c.vm.provider :virtualbox do |p|
    p.customize ["modifyvm", :id, "--memory", "1024"]
    p.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end
  c.vm.provision :chef_solo do |chef|

     chef.cookbooks_path = [DEVELOPER_BOOTSTRAP_PATH+"cookbooks", DEVELOPER_BOOTSTRAP_PATH+"site-cookbooks"]
     chef.roles_path = DEVELOPER_BOOTSTRAP_PATH+"roles"
     chef.data_bags_path = DEVELOPER_BOOTSTRAP_PATH+"data_bags"
     chef.environments_path=DEVELOPER_BOOTSTRAP_PATH+"environments"

     chef.environment="vagrant_node"
      
     chef.add_role "nodejs_complete"     
     chef.add_role "nodejs_debug"     

  end
end
