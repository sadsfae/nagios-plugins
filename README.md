nagios-plugins
===================

This is a collection of miscellaneous Nagios plugins.
   - See plugin directory README.md for requirements/install information. 

**nagios-plugin-check-libvirt**
   - Checks Sample Output of virsh list --all for running VM's
   - Errors when a VM is in a shutdown state
   - Original Credit: Karl Rink <krink@csun.edu>
   * __Sample Output__
      - `hosts:3 OK:3 WARN:0 CRIT:0 - host01:running host02:running host03:running`

**nagios-plugin-check-mdadm**
   - Checks mdadm Linux RAID status
   - Displays status if in check or rebuild state
   - Original credit: Sebastian Grewe
   * __Sample Output__
      - `OK - Checked 1 arrays`

**nagios-plugin-check-mumble**
   - Checks status of a local mumble server, used with nrpe
   - Displays status and number of connected users via DBUS
   - Modified from: http://blog.ip.v4.me.uk/mumble-murmur-nagios-plugin/
   * __Sample Output__
      - `MURMUR OK - Current Users = 3`
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
    ├── nrpe_dbus_introspect.pp
    ├── nrpe_dbus_murmur.pp
    └── nrpe_murmur.pp
```
