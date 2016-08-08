#Supported tags and respective Dockerfile links

- [`0.1.0`, `0.1.0` (*0.1.0/Dockerfile*)](https://github.com/Accenture/adop-gerrit/blob/master/Dockerfile.md)

# What is docker-gerrit?

adop-gerrit is a wrapper for the openfrontier/gerrit image. It has primarily been built to perform extended configuration.
Gerrit, web-based collaboration tool. Gerrit aims to facilitate reviews of source code in the context of a software developers in a team.

# How to use this image

The easiest way to run adop-gerrit image is as follow:
```
docker run --name <your-container-name> -d -p 8080:8080 -p 29418:29418 accenture/adop-docker-gerrit:VERSION
```
after the above gerrit will be available at: http://localhost:8080

## Run docker-gerrit with MySQL and OpenLDAP
The following assumes that MySQL and OpenLDAP are running.

The following command will run adop-gerrit and connect it to MySQL and OpenLDAP
```
  docker run \
  --name adop-gerrit \
  -p 8080:8080 \
  -p 29418:29418 \
  -e DATABASE_TYPE=mysql \
  -e DB_HOSTNAME=<mysql-servername> 
  -e DB\_PORT="3306"
  -e DB\_NAME=<mysql-dbame>
  -e DB\_USER=<mysql-dbuser>
  -e DB\_PASSWORD=<mysql-dbpassword>
  -e AUTH\_TYPE=LDAP \
  -e LDAP\_SERVER=<ldap-servername:389> \
  -e LDAP\_ACCOUNTBASE=<ldap-basedn> \
  -d accenture/adop-gerrit:VERSION
```

In addition all the LDAP attibutes defined in [Gerrit LDAP](https://gerrit-review.googlesource.com/Documentation/config-gerrit.html#ldap) are supported.

## Additional useful variables

The following variables were added for further customisation:

REINDEX if set to TRUE will perform reindexing required for Gerrit upgrades (Gerrit 2.9 contains schema changes)
SKIP_INIT if set to TRUE will skip the initialisation scripts that are run for adop-gerrit
SCREEN_UI if set to OLD_UI will revert the display UI to old version (gerrit.changeScreen = OLD_UI)  
```
  -e REINDEX=TRUE \
  -e SKIP_INIT=TRUE \
  -e SCREEN_UI=OLD_UI \
``` 
Variables were also added to configure GitBlit, RTC and Garbage Collection (GC). Eg.
```
  -e GITWEB_TYPE=custom \
  -e RTC_ENABLE_INTEGRATION=true \
  -e GC_AGGRESSIVE=false \
```
# License
Please view [licence information](LICENCE.md) for the software contained on this image.

#Supported Docker versions

This image is officially supported on Docker version 1.9.1.
Support for older versions (down to 1.6) is provided on a best-effort basis.

# User feedback

## Documentation
Documentation for this image is available in the [Gerrit documenation page](https://gerrit-review.googlesource.com/Documentation/config-gerrit.html). 
Additional documentaion can be found under the [`docker-library/docs` GitHub repo](https://github.com/docker-library/docs). Be sure to familiarize yourself with the [repository's `README.md` file](https://github.com/docker-library/docs/blob/master/README.md) before attempting a pull request.

## Issues
If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/Accenture/adop-gerrit/issues).

## Contribute
You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/Accenture/adop-gerrit/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
