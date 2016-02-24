nagios-plugin-check-libvirt
===========================

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
