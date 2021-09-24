# zx-deca

ZX Spectrum implementation on a DECA development board

## Pre-requisites

- Vagrant
- Ansible

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
```

Once the virtual machine has been provisioned and it is up and running, run the following command in the console on the guest OS:

```sh
./zx-deca/quartus/setup.sh --unattendedmodeui minimalWithDialogs --mode unattended --accept_eula 1
```
