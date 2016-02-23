nagios-plugins
===================

This is a collection of miscellaneous Nagios plugins.
```
├── nagios-plugin-check-libvirt
│   ├── check_kvm
│   └── nrpe_virsh_check.pp
├── nagios-plugin-check-mdadm
│   ├── check_raid
│   └── nrpe_mdadm.pp
└── nagios-plugin-check-mumble
    ├── check_murmur
        └── dbus-murmurd.conf
```
**nagios-plugin-check-libvirt**
   - Checks output of virsh list --all for running VM
   - Errors when a VM is in a shutdown state
   - Original Credit: Karl Rink <krink@csun.edu>
   * Requirements:
      - /etc/sudoers access for the nrpe user to run virsh list --all
         - nrpe ALL=(ALL) NOPASSWD:/usr/bin/virsh list --all
      - selinux policy module: nrpe_virsh_check.pp
         - semodule -i nrpe_virsh_check.pp
   * Installation:
      - Copy to check_libvirt /usr/lib64/nagios/plugins
      - Use via nrpe: /etc/nagios/nrpe.cfg
         - command[check_libvirt]=/usr/lib64/nagios/plugins/check_libvirt

 **nagios-plugin-check-mdadm**
   - Checks mdadm Linux RAID status
   - Displays status if in check or rebuild state
   - Original credit: Sebastian Grewe
   * Requirements: 
      - /etc/sudoers access for the nrpe user to run the check
         - nrpe ALL=(ALL) NOPASSWD:/usr/lib64/nagios/plugins/check_mdadm
      - selinux policy module: nrpe_mdadm.pp
         - semodule -i nrpe_mdadm.pp
   * Installation:
      - Copy check_mdadm to /usr/lib64/nagios/plugins
      - Use via nrpe: /etc/nagios/nrpe.cfg
         - command[check_raid]=/usr/lib64/nagios/plugins/check_raid

**nagios-plugin-check-mumble**
   - Checks status of a local mumble server, used with nrpe
   - Displays status and number of connected users via DBUS
   - Modified from: http://blog.ip.v4.me.uk/mumble-murmur-nagios-plugin/
   * Requirements:
      - Perl Packages:
         - perl-Monitoring-Plugin 
         - perl-HTML-Template
         - perl-Nagios-Plugin
         - perl-CGI
	 - perl-Net-DBus
   - Installation:
      - Copy to check_murmur to /usr/lib64/nagios/plugins
      - Set 'dbus=system' in mumble-server.ini
      - Copy associated /etc/dbus-1/system.d/murmurd.conf to system
      - Reboot (or restart DBUS without rebooting somehow)
      - Use via nrpe: /etc/nagios/nrpe.cfg
         - command[check_murmur]=/usr/lib64/nagios/plugins/check_murmur
