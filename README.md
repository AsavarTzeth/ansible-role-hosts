Ansible hosts(5) Role
=======================

**Ansible role used to manage the /etc/hosts, hosts(5) file.**

Since there is such a thing as DNS, the primary goal is to allow
managing how localhost and the local hostname is resolved. Since most
distributions now seem to use nss-myhostname, static files should be avoided
by default, however some users, somehow still experience issues.

All this being said, the role still allows custom hosts maps.

Requirements
------------

This role was developed and tested on Ansible 2.2.0 and higher.
It may work on lower versions but that is currently unsupported.

Role Variables
--------------

    # Custom dictionary mapping of ip address and hostname
    hosts_map: (default: {})

    # Enables localhost entries for ipv6
    hosts_map_ipv6: (default: true)

    # On many distributions the following options might be considered legacy.
    # Systems that use the myhostname nss plugin should not need this.
    # However, application specific issues have been reported solved this way.

    # Enables local network hostname resolution
    hosts_map_hostname: (default: false) (Debian: true)

    # Defines what address the local hostname should resolve to
    hosts_map_hostname_addr: (default: 127.0.1.1)

Dependencies
------------

None

Example Playbook
----------------

1 ) Add custom ip address mappings, using a dictionary:

    - hosts: all
      roles:
        - role: AsavarTzeth.hosts
          hosts_map:
            "192.168.1.1":
              - foo
            "192.168.1.2":
              - bar

2 ) Add local hostname to hosts file, while disabling ipv6 loopback:

    - hosts: all
      roles:
        - role: AsavarTzeth.hosts
          hosts_map_ipv6: false
          hosts_map_hostname: true
          hosts_map_hostname_addr: 127.0.0.1

License
-------

BSD-2-Clause

Author Information
------------------

Patrik Nilsson
