Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 8080, host: 8080 # atc

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2

    # dns resolution appears to be very slow in some environments; this fixes it
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  # provides aufs
  config.vm.provision "shell",
    inline: "apt-get -y install linux-image-extra-$(uname -r)"

  config.vm.provision "bosh" do |c|
    c.manifest = File.read(File.expand_path("../manifests/vagrant-bosh.yml", __FILE__))
  end
end
