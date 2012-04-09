    gewake is a script developed at NorthWest Research Associates (NWRA) to
allow machines to be shutdown when idle and automatically woken up when needed.
It works pretty well for us, but there may be aspects of it that are specific
to how we have Grid Engine setup locally.

Overview:

    gewake is run periodically from cron.  It runs qstat to see if any jobs
are waiting.  If there are, it looks for hosts that are down and wakes one
up from its list of hosts.  To do this it runs a wakeup command with the
hostname of the machine to wake up as the argument.  A sample wakeup command
is provided that uses ether-wake to send a magic WOL packet to the machine,
but it could be done in other ways.

To install:

- Edit gewake.hosts and add the hostnames you want to be woken up.
- Copy gewake.hosts to /usr/local/etc (or similar) on the machine you want
  to run the gewake monitor.  This can be any machine that can run qstat and
  is on the same LAN as the hosts to be woken up.
- Edit gewake and change $wakehostsfiles and $wakeupcmd as needed
- Copy gewake to /usr/local/bin or similar.
- Edit gewake.cron to set the grid engine environment and to point to
  where you are installing gewake
- Copy gewake.cron to /etc/cron.d
- mkdir /var/lib/gewake

To use wakeup:

- Edit etherhosts and enter the ethernet MAC addresses as shown
- Copy etherhosts to /usr/local/etc or similer.
- Copy wakeup to /usr/local/bin or similar.
- Edit /etc/sudoers to give your users permission to use wakeup if desired.
  This is not necessary for gewake unless you don't want that running as root
  in which case you will need to add that user to the sudoers file.
  This is what we do:

   ## For wakeup
   Cmnd_Alias WAKEUP = /sbin/ether-wake *

   # Don't log wakeup
   Defaults!WAKEUP !syslog

   %usergroup  ALL=NOPASSWD: WAKEUP

zz-hibernate:

    This is a script we use locally to shut down idle machines.  We run it
from /etc/cron.hourly.  It probably will need to get modified for local
paths and preferences.

Author:

  Orion Poplawski <orion@cora.nwra.com>
