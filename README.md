netdev-backup
=============

Script which logs into your network devices (routers, switches etc.),
downloads the current configuration and stores it in a git repository.

Installation and Usage
----------------------

In order to use netdev-backup, you first have to create a git
repository which will hold your configuration backups:

```
git init --bare <path-to-repository>
```

Then, create config.cfg and hosts.cfg files and put these in the new
repository as well.

Now, you can call netdev-backup as follows:

```
netdev-backup <path-to-repository>
```

This command will do the following:

- Clone into you repository.
- Read your config.cfg and hosts.cfg.
- Log into all the network devices defined in hosts.cfg to download
  the configurations.
- Commit all configurations to the repository.
- Send an email with a report (if this is configured in config.cfg).

It is also possible to specify the config.cfg and hosts.cfg files on
the command line. In order to see a list of all command line switches,
call netdev-backup without arguments or with _--help_.

Configuration file: config.cfg
------------------------------

The config.cfg file is stored in the repository or specified on the
command line.

It contains one _key=value_ pair per line. Content after # is ignored
(comment).

The following keys are supported:

- **report_subject**: Subject of the report email
- **report_from**: From address of the report email
- **report_to**: Recipient of the report email (comma-separated for
  multiple recipients

List of network devices: hosts.cfg
----------------------------------

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
- **mikrotik**: Mikrotik routers. Important append "+ct" to the username
  to switch off the fancy colors and other terminal stuff.

Supported protocols:

- **ssh**: SSH
- **ssh-des**: SSH with the DES cipher
- **ssh-3des**: SSH with the 3DES cipher
- **telnet**: Telnet
