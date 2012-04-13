=================================================================
netconfig - distribution independent network configuration script
=================================================================

netconfig is distribution independent network configuration script for linux.
It uses own DSL to define network.


requirements
============

- bash
- iproute2 (for interface and route)
- bridge-utils (for bridge)
- shelltestrunner (for tests)


usage
=====

::

  usage: netconfig [options] [CONFIG_FILE...]
  options:
      -h                  display this help
      -n                  dry-run
      -v                  verbose error output
      -m <start|stop>     set mode (default: start)
      -t TARGET           only apply config for specific TARGET
      -c 'CONFIG STRING'  use 'CONFIG STRING' instead of reading CONFIG_FILE


example
=======

Put config file like below,

``/etc/netconfig.conf``::

  define interface eth0
    address   192.168.0.11
    netmask   255.255.255.0
    broadcast 192.168.0.255
  end

  define route default
    via 192.168.0.1
  end

and call ``netconfig``.

netconfig read the config file, translate to commands like below and execute these::

  /sbin/ip link set eth0 up
  /sbin/ip addr add 192.168.0.11/255.255.255.0 broadcast 192.168.0.255 dev eth0
  /sbin/ip route add default via 192.168.0.1
