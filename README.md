## Few things to help working with Lustre without access to a large physical cluster

### Creating a AWS AMI image with Lustre built on it for use in deploying a cluster on AWS

1. Create an EC2 instance with RHEL9 or 8. RHEL10 will have a kernel for which lustre won't want to build certain modules(ie: ldiskfs)
2. Login and run the following commands to build lustre on it, this will be used for all server and client nodes, specific configuration will be done after
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

  git clone https://github.com/lustre/lustre-release.git
  cd lustre-release

  sh autogen.sh


