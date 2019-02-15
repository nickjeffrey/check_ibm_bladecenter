# check_bladecenter
nagios check for IBM BladeCenter chassis health

# Requirements
You will need to enable SNMP on the BladeCenter Management Module.

Login to the web interface of the Management Module, then click MM Control, Network Protocols, SNMP.

Add the following section to the commands.cfg file.  
```
define command {
  command_name      check_bladecenter
  command_line      $USER1$/check_bladecenter -C public -H $HOSTADDRESS$ -c $ARG1$ 
}
```

Add the following section to the services.cfg file.
```
# -----------------------------------------------------------
#  misc checks on BladeCenter Advanced Management Module
# -----------------------------------------------------------
define service {
       use                             generic-24x7-service
       hostgroup_name                  all_amm
       service_description             BladeCenter health 
       check_command                   check_bladecenter!public
       }
```

Save the perl script as `/usr/local/nagios/libexec/check_bladecenter` (or wherever your distro keeps nagios checks)
