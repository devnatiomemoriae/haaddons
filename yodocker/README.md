# yodocker

yodocker is a simple Home Assistant add-on which allows any number of docker-compose commands to be run upon add-on startup. In addition, files can be nominated to be monitored for writes and can trigger re-execution of the configured docker-compose commands.

If you like the simplicity and familiarity of using docker-compose and would prefer to use regular docker containers instead of docker containers by way of Home Assistant Add-ons, then this add-on could be of use to you.

Consider using Portainer stacks or similar instead of this add-on.

WARNING: This add-on assumes you understand the risks of using docker and isn't afraid to open up some attack vectors.