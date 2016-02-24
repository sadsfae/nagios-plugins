nagios-plugins
===================

This is a collection of miscellaneous Nagios plugins.

**nagios-plugin-check-libvirt**
   - Checks output of virsh list --all for running VM's
   - Errors when a VM is in a shutdown state
   - Original Credit: Karl Rink <krink@csun.edu>
   * __Requirements:__
      - /etc/sudoers access for the nrpe user to run virsh list --all
         - `nrpe ALL=(ALL) NOPASSWD:/usr/bin/virsh list --all`
      - selinux policy module: nrpe_virsh_check.pp
   * __Installation:__
      - Apply selinux policy
         * `semodule -i nrpe_virsh_check.pp`
      - Copy `check_libvirt` to `/usr/lib64/nagios/plugins`
      - Use via nrpe: /etc/nagios/nrpe.cfg
         * `command[check_libvirt]=/usr/lib64/nagios/plugins/check_libvirt`
   * __Output__
      - `hosts:3 OK:3 WARN:0 CRIT:0 - host01:running host02:running host03:running`

**nagios-plugin-check-mdadm**
   - Checks mdadm Linux RAID status
   - Displays status if in check or rebuild state
   - Original credit: Sebastian Grewe
   * __Requirements:__ 
      - /etc/sudoers access for the nrpe user to run the check
         - `nrpe ALL=(ALL) NOPASSWD:/usr/lib64/nagios/plugins/check_mdadm`
      - selinux policy module: nrpe_mdadm.pp
   * __Installation:__
      - Apply selinux policy
         * `semodule -i nrpe_mdadm.pp`
      - Copy `check_mdadm` to `/usr/lib64/nagios/plugins`
      - Use via nrpe: /etc/nagios/nrpe.cfg
         * `command[check_raid]=/usr/lib64/nagios/plugins/check_raid`
   * __Output__
      - `OK - Checked 1 arrays`

**nagios-plugin-check-mumble**
   - Checks status of a local mumble server, used with nrpe
   - Displays status and number of connected users via DBUS
   - Modified from: http://blog.ip.v4.me.uk/mumble-murmur-nagios-plugin/
   * __Requirements:__
      - Perl Packages:
         - perl-Monitoring-Plugin 
         - perl-HTML-Template
         - perl-Nagios-Plugin
         - perl-CGI
         - perl-Net-DBus
      - selinux policy modules:
         - nrpe_murmur.pp, nrpe_dbus_murmur.pp, nrpe_dbus_introspect.pp
   * __Installation:__
      - Apply selinux policies (DBUS is an AVC minefield)
         * `semodule -i nrpe_murmur.pp`
         * `semodule -i nrpe_dbus_murmur.pp`
         * `semodule -i nrpe_dbus_introspect.pp`
      - Copy `check_murmur` to `/usr/lib64/nagios/plugins`
      - Set `dbus=system` in `mumble-server.ini`
      - Copy `dbus-murmurd.conf` to `/etc/dbus-1/system.d/`
      - Reboot (or restart DBUS without rebooting somehow)
      - Use via nrpe: /etc/nagios/nrpe.cfg
         * `command[check_murmur]=/usr/lib64/nagios/plugins/check_murmur`
    * __Output__
        - `MURMUR OK | users=3;;`
```
├── nagios-plugin-check-libvirt
│   ├── check_libvirt
│   └── nrpe_virsh_check.pp
├── nagios-plugin-check-mdadm
│   ├── check_raid
│   └── nrpe_mdadm.pp
└── nagios-plugin-check-mumble
    ├── check_murmur
    ├── dbus-murmurd.conf
    └── nrpe_murmur.pp
```
