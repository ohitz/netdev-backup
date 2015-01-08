netdev-backup
=============

Script which logs into your network devices (routers, switches etc.),
downloads the current configuration and stores it in a git repository.

config.cfg
----------

The config.cfg file is stored in the repository or specified on the
command line.

It contains one _key=value_ pair per line.

The following keys are supported:

- **report_subject**: Subject of the report email
- **report_from**: From address of the report email
- **report_to**: Recipient of the report email (comma-separated for
  multiple recipients

hosts.cfg
---------

The hosts.cfg file stored in the repository or specified on the
command line contains the list of network devices to log into. Every
host is specified on one line using a comma separated list of
_key=value_ pairs:

key1=value1,key2=value2,key3=value3,...

Content after # is considered as comment.

The following keys are available:

- **name**: Name of the network device
- **ip**: IP address of the network device
- **user**, **password**: Username and password (in cleartext) used
  for logging in
- **enable**: Enable password
- **type**: Device type (see below)
- **protocol**: Protocol to use for accessing the device (see below)
- **backup_ip**, **backup_port**: IP address and port if the IP
  specified in **ip** is not directly reachable by netdev-backup
  (i.e. it is hidden behind some other device)

Supported device types:

- **cisco**: Cisco IOS boxes
- **iosxr**: Cisco IOS XR boxes
- **ciscosg**: Cisco Small Business switches
- **pix**: Cisco Pix firewalls
- **foundry**: Foundry and Brocade switches
- **hp**: HP Procurve switches

Supported protocols:

- **ssh**: SSH
- **ssh-des**: SSH with the DES cipher
- **ssh-3des**: SSH with the 3DES cipher
- **telnet**: Telnet
