A simple `Vagrant` image with squid setup for ones who provision their machines frequently and want to save some time and traffic.

How to use
---

1. Spin the machine up with `vagrant up`
2. Set up your other VMs to use `192.168.56.250:3128` as an http proxy server

For the latter you could use `vagrant-proxyconf` vagran plugin or any other that helps automate specifying VM proxy servers.

In case of `vagrant-proxyconf` just add the following lines into your `Vagrantfile`:

    config.proxy.http     = "http://192.168.56.250:3128"
    config.apt_proxy.http = "http://192.168.56.250:3128"
    config.apt_proxy.https= "DIRECT"

Some notes
---

At this moment the IP address is hardcoded to be `192.168.56.250`, but if someone else but me will use this VM and they will not be happy with the given IP address - I could modify it to use environment variables instead.