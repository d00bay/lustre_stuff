## Few things to help working with Lustre without access to a large physical cluster

### Creating a AWS AMI image with Lustre built on it for use in deploying a cluster on AWS

1. Create an EC2 instance with RHEL9 or 8. RHEL10 will have a kernel for which lustre won't want to build certain modules(ie: ldiskfs)
2. Login and run the following commands to prepare the system to build Lustre(#3)
```sudo dnf groupinstall "Development Tools" -y
    sudo dnf install -y \
    kernel-devel-$(uname -r) \
    kernel-headers-$(uname -r) \
    libtool \
    automake \
    autoconf \
    asciidoc \
    xmlto \
    libyaml-devel \
    libaio-devel \
    libblkid-devel \
    libselinux-devel \
    readline-devel \
    e2fsprogs-devel \
    elfutils-libelf-devel \
    elfutils-devel \
    bison \
    flex \
    patch \
    rpm-build \
    git \
    gcc \
    gcc-c++

    sudo dnf install -y keyutils-libs-devel libmount-devel libnl3-devel

 ## Without a RH subscription, libyaml needs to be built manually
 curl -LO https://github.com/yaml/libyaml/releases/download/0.2.5/yaml-0.2.5.tar.gz
 tar xzf yaml-0.2.5.tar.gz
cd yaml-0.2.5
./configure --prefix=/usr
make -j$(nproc)
sudo make install



  sudo dnf install kernel
  sudo reboot
```
3. Log back in after the latest kernel has been booted. Run the following commands to build Lustre
```
  git clone https://github.com/lustre/lustre-release.git
  cd lustre-release

  sh autogen.sh


