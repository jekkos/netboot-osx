Tftpboot for OSX Netboot firmware
=================================

Concept
-------
This repo contains file + dnsmasq configuration that can be used to netboot an OSX system through its built in tftp client.

I tried to use this functionality to boot a MacbookPro with a completely messed up EFI partition from the network, as the faulty partition would crash the firmware upon loading.

You will need to server the files  using dnsmasq and the included dnsmasq.conf file. Basic commands to get up and running are the following.

Setup
-----
    sudo apt-get install dnsmasq
    dnsmasq -C dnsmasq.conf -d

The -d option will prevent dnsmasq from daemonizing and will output debug info to stdout (terminal)
