# Install required plugins
required_plugins = %w(vagrant-hostsupdater vagrant-berkshelf) # this plugin allows vagrant to run chef cookbook for us
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder "Python-Sample-Application-master", "/home/ubuntu/Python-Sample-Application-master"
    #app.vm.provision "shell", path: "environment/app/provision.sh", privileged: false
    app.vm.provision "chef_solo" do |chef|
      chef.arguments = "--chef-license accept"
      chef.add_recipe "nginx::default"
      chef.add_recipe "python::default"
    end
  end
end
  # config.vm.define "db" do |db|
  #   db.vm.box = "ubuntu/xenial64"
  #   db.vm.network "private_network", ip: "192.168.10.150"
  #   db.vm.synced_folder "environment/db", "/home/ubuntu/environment"
  #   db.vm.provision "chef_solo" do |chef|
  #     # chef.arguments = "--chef-license accept"
  #     # chef.add_recipe "nginx::default"

#   end
# end
