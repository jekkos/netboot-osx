tftpboot for OSX Netboot firmware
=================================

Concept
-------
This repo contains file + dnsmasq configuration that can be used to netboot an OSX system through its built in tftp client.

I tried to use this functionality to boot a MacbookPro with a completely messed up EFI partition from the network, as the faulty partition would crash the firmware upon loading.

You will need to server the files using dnsmasq and the included dnsmasq.conf file. Basic commands to get up and running are the following.

The [original post](http://lists.thekelleys.org.uk/pipermail/dnsmasq-discuss/2010q1/003638.html) was found in the dnsmasq mailing lists, which contains a more or less working config file to server macs with a netboot image.

NFS root filesystem
-------------------
The actual filesystem will be sent through a specific DHCP option to the requesting client, after the bootloader files have been transferred and loaded into memory. This image can be created for free with just an existing os x installation using os x server or [DeployStudio](http://www.deploystudio.com).

Apple's broken tftp implementation
----------------------------------
During this setup I did experience that the mac firmware's tftp client is very picky about the negotiated tftp options. The implementation is really broken and doesn't adhere to what a normal tftp client would expect. I tried different tftp clients and ended up using WireShark to see where the transfer went wrong. Sadly dnsmasq only allows you to disable the tftp packet size negotation, which caused the tftp apple client to abort the transfer too soon.


Setup
-----
```
    sudo apt-get install dnsmasq
    dnsmasq -C dnsmasq.conf -d
```

The -d option will prevent dnsmasq from daemonizing and will output debug info to stdout (terminal)
