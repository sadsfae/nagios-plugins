nagios-plugin-check-madm
========================

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
      - `OK - Checked 1 arrays, check : 5.9%`
