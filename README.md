# nexus-yum-isolated-test

----------


## Purpose 
Many companies/organizations lock down server's access to the internet.  This simple project allows testing of centos configuration for yum pointing to nexus as a proxy.  Verifies that centos is limited to only communicate to nexus repo. Thus allows yum.repos.d modification to be tested.

## Overview
Takes Sonatype 3.9.0 docker image and a stand alone centos docker image. Creates 2 networks one has internet access and the other does not.  The centos image is attached to "no-internet" network while the nexus image can communicate on both "internet" and "no-internet" network

This was created based on the document offered by sonatype. https://help.sonatype.com/repomanager3/yum-repositories

## Run

```
git clone https://github.com/doughoke/nexus-yum-isolated-test.git
```
Now go to the new directory and docker compose up.

```
cd nexus-yum-isolated-test
docker-compose up
```

The nexus repo should be running on http://localhost:8081

login with:
admin/admin123

set up your yum repo to point http://mirror.centos.org/centos/ (or whatever repo mirror you want)

ssh into the centos container
```
docker exec -it centos-no-internet /bin/bash
```

inside the container cd to /etc/yum.repos.d
back up existing .repo files
create a new repo file pointing to nexus (note use the sha of the nexus container