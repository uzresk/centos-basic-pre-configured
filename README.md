# CentOS of the basic pre-configured 

Start CentOS6 or CentOS7 using vagrant ansible_local provisioner.
Set the locale and timezone in playbook.

## Requires

1. Oracle VirtualBox
2. Vagrant1.8.1 later

## Usage

* How to use is very easy

### install VirtualBox and Vagrant1.8.1 later

* [OracleVirtualBox Download](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html?ssSourceSiteId=otnjp)
* [Vagrant Download](https://www.vagrantup.com/downloads.html)

### Get the code

`$ git clone https://github.com/uzresk/centos-basic-pre-configured.git`

### Start CentOS

`$ vagrant up`

---

### Configuration

* Host name, IP address , box file, please edit the vagrantfile

```Vagrantfile
Vagrant.configure(2) do |config|
  config.vm.define "base" do |node|
        node.vm.box = "bento/centos-6.7"
        node.vm.hostname = "base"
        node.vm.network :private_network, ip: "192.168.1.10"
  end
  config.vm.network "forwarded_port", id: "ssh", guest: 22, host: 2223, auto_correct: true
  if ARGV[0] == 'up'
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "site.yml"
    end
  end
  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http = "http://xxxxx:8080/"
    config.proxy.https = "http://xxxxx:8080/"
    config.proxy.no_proxy = "localhost,127.0.0.1,10.0.0."
  end
end
```
