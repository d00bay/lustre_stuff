# Setting up a small cluster with qemu for testing/learning

1. Install the required packages locally. I use void linux so I'm posting the commands for this, please find the right cmds for your distro(on the host)

`sudo xbps-install -Suy
sudo xbps-install -y \
  qemu libvirt virt-manager virt-install \
  bridge-utils dnsmasq iptables-nft dbus \
  cloud-utils genisoimage
`

2. Set up a bridge for the Lustre cluster network on the host
`sudo ip link add br-lustre type bridge
sudo ip addr add 192.168.100.1/24 dev br-lustre
sudo ip link set br-lustre up
`

2. Set up a golden image to be used for mds/oss/client. I use Rocky 9.7 so I downloaded the iso

   


4. 
