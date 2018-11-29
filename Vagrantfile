# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  pe_version                    = '2019.0.0'
  config.pe_build.version       = pe_version

######################
## Puppet Master VM ##
######################
  # Define the Master VM Characteristics
  config.vm.define 'master' do |master|
    master.vm.box = 'centos/7'
    master.vm.network :private_network, :ip => '10.10.100.100'
    master.vm.network "forwarded_port", guest: 443, host: 8443
    master.vm.hostname = 'master.puppetlabs.vm'

  # Configure Master VM Settings
  master.vm.provider :virtualbox do |settings|
    settings.memory = 4608
    settings.name = "master_2019.0.0"
    settings.cpus = 2
  end

  # Add all other hosts for environment
  master.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm', 'master']
    entries.add_host '10.10.100.110', ['centos6.puppetlabs.vm', 'centos6']
    entries.add_host '10.10.100.111', ['centos7.puppetlabs.vm', 'centos7']
    entries.add_host '10.10.100.112', ['trusty.puppetlabs.vm', 'trusty']
    entries.add_host '10.10.100.113', ['xenial.puppetlabs.vm', 'xenial']
  end

  # Set the PE Role for this node
  master.vm.provision :pe_bootstrap do |provisioner|
    provisioner.role = :master
    provisioner.answer_file = 'provision/pe.conf'
  end
    master.vm.provision :shell, path: "provision/master.sh"
  end

################
## CentOS6 VM ##
################
  # Define the CentOS6 VM Characteristics
  config.vm.define 'centos6' do |centos6|
    centos6.vm.box = 'centos/6'
    centos6.vm.network :private_network, :ip => '10.10.100.110'
    centos6.vm.hostname = 'centos6.puppetlabs.vm'

  # Configure CentOS6 VM Settings
  centos6.vm.provider :virtualbox do |settings|
    settings.memory = 1024
    settings.name   = "c6_ossec_pe2019.0.0"
    settings.cpus   = 1
  end

  # Add all other hosts for environment
  centos6.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm',  'master' ]
    entries.add_host '10.10.100.110', ['centos6.puppetlabs.vm', 'centos6']
    entries.add_host '10.10.100.111', ['centos7.puppetlabs.vm', 'centos7']
    entries.add_host '10.10.100.112', ['trusty.puppetlabs.vm',  'trusty' ]
    entries.add_host '10.10.100.113', ['xenial.puppetlabs.vm',  'xenial' ]
  end

  # Set the PE Role of This Node
  centos6.vm.provision :pe_agent do |provisioner|
    provisioner.master = 'master.puppetlabs.vm'
  end
    centos6.vm.provision :shell, path: "provision/centos6.sh"
  end

################
## CentOS7 VM ##
################
  # Define the CentOS7 VM Characteristics
  config.vm.define 'centos7' do |centos7|
    centos7.vm.box = 'centos/7'
    centos7.vm.network :private_network, :ip => '10.10.100.111'
    centos7.vm.hostname = 'centos7.puppetlabs.vm'

  # Configure CentOS7 VM Settings
  centos7.vm.provider :virtualbox do |settings|
    settings.memory = 1024
    settings.name   = "c7_ossec_pe2019.0.0"
    settings.cpus   = 1
  end

  # Add all other hosts for environment
  centos7.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm',  'master' ]
    entries.add_host '10.10.100.110', ['centos6.puppetlabs.vm', 'centos6']
    entries.add_host '10.10.100.111', ['centos7.puppetlabs.vm', 'centos7']
    entries.add_host '10.10.100.112', ['trusty.puppetlabs.vm',  'trusty' ]
    entries.add_host '10.10.100.113', ['xenial.puppetlabs.vm',  'xenial' ]
  end

  # Set the PE Role of This Node
  centos7.vm.provision :pe_agent do |provisioner|
    provisioner.master = 'master.puppetlabs.vm'
  end
    centos7.vm.provision :shell, path: "provision/centos7.sh"
  end

###############
## Trusty VM ##
###############
  # Define the Trusty 14.04 VM Characteristics
  config.vm.define 'trusty' do |trusty|
    trusty.vm.box = 'ubuntu/trusty64'
    trusty.vm.network :private_network, :ip => '10.10.100.112'
    trusty.vm.hostname = 'trusty.puppetlabs.vm'

  # Configure Trusty VM Settings
  trusty.vm.provider :virtualbox do |settings|
    settings.memory = 1024
    settings.name = "trusty_ossec_pe2019.0.0"
    settings.cpus = 1
  end

  # Add all other hosts for environment
  trusty.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm',  'master' ]
    entries.add_host '10.10.100.110', ['centos6.puppetlabs.vm', 'centos6']
    entries.add_host '10.10.100.111', ['centos7.puppetlabs.vm', 'centos7']
    entries.add_host '10.10.100.112', ['trusty.puppetlabs.vm',  'trusty' ]
    entries.add_host '10.10.100.113', ['xenial.puppetlabs.vm',  'xenial' ]
  end

  # Set the PE Role of This Node
  trusty.vm.provision :pe_agent do |provisioner|
    provisioner.master = 'master.puppetlabs.vm'
  end
    trusty.vm.provision :shell, path: "provision/trusty.sh"
  end

###############
## Xenial VM ##
###############
  # Define the Xenial 16.04 VM Characteristics
  config.vm.define 'xenial' do |xenial|
    xenial.vm.box = 'ubuntu/xenial64'
    xenial.vm.network :private_network, :ip => '10.10.100.113'
    xenial.vm.hostname = 'xenial.puppetlabs.vm'

  # Configure Xenial VM Settings
  xenial.vm.provision :hosts do |settings|
    settings.memory = 1024
    settings.name   = "xenial_ossec_pe2019.0.0"
    settings.cpu    = 1
  end

  # Add all other hosts for environment
  trusty.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm',  'master' ]
    entries.add_host '10.10.100.110', ['centos6.puppetlabs.vm', 'centos6']
    entries.add_host '10.10.100.111', ['centos7.puppetlabs.vm', 'centos7']
    entries.add_host '10.10.100.112', ['trusty.puppetlabs.vm',  'trusty' ]
    entries.add_host '10.10.100.113', ['xenial.puppetlabs.vm',  'xenial' ]
  end

  # Set the PE Role of This Node
  xenial.vm.provision :pe_agent do |provisioner|
    provisioner.master = 'master.puppetlabs.vm'
  end
    xenial.vm.provision :shell, path: "provision/xenial.sh"
  end
end
