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
