# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "precise" do |precise|
    precise.vm.box = "ubuntu/precise64"
  end

  config.vm.define "trusty" do |trusty|
    trusty.vm.box = "ubuntu/trusty64"
  end

  config.vm.define "jessie" do |jessie|
    jessie.vm.box = "debian/contrib-jessie64"
    jessie.vm.synced_folder ".", "/vagrant",
      type: 'virtualbox'
  end

  config.ssh.forward_agent = true
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
  end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "package.yml"
     ansible.host_key_checking = false
     ansible.sudo = true

     ansible.verbose = ENV.fetch("CKAN_PACKAGE_ANSIBLE_VERBOSE", "vv")
     ansible.extra_vars = {}

     ansible.extra_vars["datapusher"] = ENV.fetch("CKAN_PACKAGE_DATAPUSHER", "y")

     if ENV.has_key?("CKAN_PACKAGE_VERSION")
         ansible.extra_vars["version"] = ENV["CKAN_PACKAGE_VERSION"]
     end
     if ENV.has_key?("CKAN_PACKAGE_ITERATION")
         ansible.extra_vars["iteration"] = ENV["CKAN_PACKAGE_ITERATION"]
     end
   end
end
