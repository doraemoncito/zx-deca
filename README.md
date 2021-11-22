# zx-deca

ZX Spectrum implementation on a DECA development board.

Please note that this project no longer creates a VM with a graphics driver as this had significant performance implications, instead you'll need to connect to the virtual machine using remote desktop. 

## Development environment pre-requisites

- [VirtualBox](https://www.virtualbox.org)
- [Vagrant](https://www.vagrantup.com)
- [Vagrant VirtualBox guest plug-in](https://github.com/dotless-de/vagrant-vbguest)
- [Ansible](https://www.ansible.com)
- [Intel's Quartus FPGA software](https://fpgasoftware.intel.com/?edition=lite)
- [Microsoft remote desktop application for macOS](https://apps.apple.com/gb/app/microsoft-remote-desktop/id1295203466?mt=12)

On macOS, the tools required to build the cross-compilation development environment for Raspberry Pi can be easily installed using the brew package manager. e.g.

```sh
echo
echo "Installing the Brew package manager"
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo
echo "Installing VirtualBox"
brew cask install virtualbox

echo
echo "Installing Vagrant"
brew cask install vagrant

# (optional) delete the installation of curl bundled with Vagrant if it causes problems when initialising Vagrant boxes
sudo rm -f /opt/vagrant/embedded/bin/curl

echo "Installing Vagrant's VirtualBox guest plug-in (https://github.com/dotless-de/vagrant-vbguest)"
vagrant plugin install vagrant-vbguest

echo "Installing the Ansible infrastructure tool"
brew install ansible
```

## Creating the development environment

Download `Quartus-lite-20.1.1.720-linux.tar` from [Intel's website](https://fpgasoftware.intel.com/?edition=lite) and place it in the quartus directory within this project.

Then, run these commands from the project's top level directory:

```sh
cd vagrant
vagrant up --provision
```

If you have more than one network interface, Vagrant will ask you to select the default one.  e.g.

```console
==> zx-deca-development-environment: Available bridged network interfaces:
1) en0: Wi-Fi (Wireless)
2) en5: USB Ethernet(?)
3) ap1
4) awdl0
5) llw0
6) en1: Thunderbolt 1
7) en2: Thunderbolt 2
8) en3: Thunderbolt 3
9) en4: Thunderbolt 4
10) bridge0
11) en7: USB 10/100/1000 LAN
==> zx-deca-development-environment: When choosing an interface, it is usually the one that is
==> zx-deca-development-environment: being used to connect to the internet.
==> zx-deca-development-environment: 
    zx-deca-development-environment: Which interface should the network bridge to? 
```

Once the virtual machine has been provisioned, rebooted, and it is up and running, run the command shown below in a console window in the guest OS.  You can connect to the guest OS using Microsoft remote desktop and the [configuration file supplied with this project](vagrant/zx-deca-development-environment.rdp).

```sh
./install_quartus.sh
```

- [ForoFPGA: Foro de cacharreo con FPGAs, CPLDs y demás tipos de lógica programable](http://www.forofpga.es/index.php)

