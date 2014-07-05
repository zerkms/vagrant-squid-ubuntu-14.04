VAGRANTFILE_API_VERSION = "2"

$setup = <<-SCRIPT

sed -i "/mirror:\\/\\//d" /etc/apt/sources.list
sed -i "1ideb mirror://mirrors.ubuntu.com/mirrors.txt trusty main restricted universe multiverse" /etc/apt/sources.list
sed -i "1ideb mirror://mirrors.ubuntu.com/mirrors.txt trusty-updates main restricted universe multiverse" /etc/apt/sources.list
sed -i "1ideb mirror://mirrors.ubuntu.com/mirrors.txt trusty-backports main restricted universe multiverse" /etc/apt/sources.list
sed -i "1ideb mirror://mirrors.ubuntu.com/mirrors.txt trusty-security main restricted universe multiverse" /etc/apt/sources.list

apt-get update

apt-get install squid -y --no-install-recommends
stop squid3

mkdir /vagrant/cache -p
mv /etc/squid3/squid.conf /etc/squid3/squid.conf.orig
cp /vagrant/squid.conf /etc/squid3/squid.conf
sed -i "/vagrant\\/cache/d" /etc/init/squid3.conf
sed -i "/pre-start/a \\\twhile [ ! -d \\"/vagrant/cache\\" ]; do sleep 5; done" /etc/init/squid3.conf

squid3 -z
while [ ! -d "/vagrant/cache/0F/FF" ]; do sleep 5; done
start squid3

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty32"

  config.vm.network "private_network", ip: "192.168.56.250"
  
  config.vm.provision "shell", inline: $setup
end
