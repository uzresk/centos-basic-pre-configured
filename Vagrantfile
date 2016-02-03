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
    config.proxy.http = "http://PROXY_HOST:PROXY_PORT/"
    config.proxy.https = "http://PROXY_HOST:PROXY_PORT/"
    config.proxy.no_proxy = "localhost,127.0.0.1,10.0.0."
  end
end
