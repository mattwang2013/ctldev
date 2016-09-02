# Registry

This catalogue item consists of a Registry, and the Portus web UI for 
authentication.  There is also a MySQL database for storage, and a nginx
proxy to provide SSL for the web frontend.

This version mounts volumes from Convoy rather than using shared mounts.
A common prefix is expected for the volumes to be created.

If no certificates are provided in the /certs directory, then the system 
will generate self-signed SSL certificates to use.

Note that the containers will take a significant amount of time to initialse after 
they are started.  You may need to wait 15 minutes for the Portus instance
to finally spot the registry instance and perform its first synchronisation,
after which the web interface will come online.

## Backing Store

A set of Convoy volues are used to host the Registry, and also the 
MySQL database, as well as the certificates under certs/server.crt
and certs/server.key; 

## Security

All connections are protected by SSL.  A self-signed certificate is
automatically generated as certs/server.crt and certs/server.key in 
the persistent shared storage; this can be replaced if necessary.

The certificate is used for registry access, for web admin access,
and for signing API access keys.

Registry access is controlled by the same user access as the web interface;
so if you link to LDAP then this will also lock the Registry access.


## Access

The template will create a Load Balancer for access to the Registry and
to the Web Admin interface.  This will run on all Hosts without the label 
LB=0, listening on the defined ports.

To access the web UI, use https on the hostname and port you configured.

To upload to the repository, use an SSL connection to the hostname and
registry port you configured.

## Administration

The first user to log in to the web interface will be granted Admin
privileges.
