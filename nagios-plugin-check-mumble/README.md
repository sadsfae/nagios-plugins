nagios-plugin-check-mumble
==========================

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
