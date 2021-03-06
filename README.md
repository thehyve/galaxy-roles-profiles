#Galaxy roles profiles
####Tables of Contents
1. [Overview](#overview)
2. [Module Description](#module-description)
3. [Setup](#setup)
    * [First step with Galaxy Roles Profiles](#first-step)
4. [Usage - The classes,roles and profiles available for configuration ](#usage)
    * [Classes](#classes)
    * [Roles](#roles)
        * [Role galaxy-roles-profiles::role::galaxy-sqlite](#role-galaxy_roles_profilesrolegalaxy-sqlite)
        * [Role galaxy_roles_profiles::role::galaxy-postgresql](#role-galaxy_roles_profilesrolegalaxy-postgresql)
        * [Role galaxy-roles-profiles::role::galaxy-apache-sqlite](#role-galaxy_roles_profilesrolegalaxy-apache-sqlite)
        * [Role galaxy-roles-profiles::role::galaxy-apache-postgresql](#role-galaxy_roles_profilesrolegalaxy-apache-postgresql)
    * [Profiles](#profiles)
        * [Profile galaxy-roles-profiles::profile::sqlite](#profile-galaxy_roles_profilesprofilesqlite)
        * [Profile galaxy-roles-profiles::profile::common](#profile-galaxy_roles_profilesprofilecommon)
        * [Profile galaxy-roles-profiles::profile::pgsql](#profile-galaxy_roles_profilesprofilepgsql)
        * [Profile galaxy-roles-profiles::profile::apache](#profile-galaxy_roles_profileprofileapache)
        * [Profile galaxy_roles_profile::profile::galaxy](#profile-galaxy_roles_profileprofilegalaxy)
5. [Deal with Hiera configuration files](#hiera)
6. [Github Projects](#github-projects)
7. [Contacts](#contact)
8. [Galaxy Project](#galaxy-project)

##Overview
This module install and configure a new instance of Galaxy. Today, there are three roles (three configuration) you can choose.

##Module Description
This is the galaxy-roles-profiles module. Galaxy is an open, web-based platform for accessible, reproducible, and transparent computational biomedical research.
This module contains roles and profiles for a Galaxy server configuration management.
It uses base blocks hosted in the Galaxy module: https://forge.puppetlabs.com/urgi/galaxy

##Setup
**what this module affect:**
* Create a new user, galaxy
* Create directories
* Manage configurations files
* Enable apache
 * see https://forge.puppetlabs.com/puppetlabs/apache for further information

###First step
Download from the Puppet Forge : https://forge.puppetlabs.com/urgi/galaxy_roles_profiles.

Configure Hiera. (See 6.Deal with Hiera).

How to install existing role:
-In a file.pp

```puppet
	include galaxy-roles-profiles::role::<the role wich you want>
```
-In the terminal

```
	puppet apply -e "include galaxy-roles-profiles::role::<the role wich you want>"
```


##Usage
###Classes
###Roles
Roles contains only one or many profiles.
 
####Role: `galaxy_roles_profiles::role::galaxy-sqlite`
Galaxy with SQLite.

```
	puppet apply -e "include galaxy_roles_profiles::role::galaxy-sqlite"
```

####Role `galaxy_roles_profiles::role::galaxy-postgresql`
Galaxy with PostgreSQL
```
	puppet apply -e "include galaxy_roles_profiles::role::galaxy-postgresql"
```

####Role: `galaxy_roles_profiles::role::galaxy-apache-sqlite`
Galaxy with SQLite and Apache.

```
	puppet apply -e "include galaxy-roles-profiles::role::galaxy-apache-sqlite"
```
####Role: `galaxy_roles_profiles::role::galaxy-apache-postgresql`
Galaxy with PostgreSQL and Apache.

```
	puppet apply -e "include galaxy_roles_profiles::role::galaxy-apache-sqlite-postgresql"
```

###Profiles
Profiles contains one or many building-block (for example galaxy::universe). One profile is one technology layer.

####Profile: `galaxy_roles_profiles::profile::sqlite`
This profile call galaxy::create_db.

####Profile: `galaxy_roles_profiles::profile::common`
This profile install Galaxy using base blocks from urgi/galaxy module.
This profile manage toolshed_conf, job_conf and universe_wsgi.ini.
You can change your config using Hiera and write  in .yaml what you want.

####Profile: `galaxy_roles_profiles::profile::postgresql`
This profile install packages for postgresql, and configure it for add a new database for galaxy.
This uses the puppetlabs/postgresql module.
These are set in a Hiera file. ( see 6.Hiera ).
Further information available at : https://forge.puppetlabs.com/puppetlabs/postgresql .

####Profile: `galaxy_roles_profiles::profile::apache`
This profile install and configure apache to deal with Galaxy.
This uses puppetlabs/apache module to install apache, create a Virtual Host and load the needed mods
To deal with balancer configuration file, we write a template ( balancer_galaxy.conf.erb ) and a class `galaxy-roles-profiles::balancer-config`
Further information available at : https://forge.puppetlabs.com/puppetlabs/apache .

####Profile: `galaxy_roles_profiles::profile::galaxy`
This profile call galaxy::service to start galaxy as service.

##Hiera
First you have to edit the hiera.yaml in /etc/hiera.yaml and in /etc/puppet/hiera.yaml (for example delete each lines in hierarchy and add "common" ).

Next you have to have one hiera file in /var/lib/hiera/ ( for example common.yaml)

You can use a sample of common.yaml and modify it as you want :

$ cp /etc/puppet/modules/galaxy_roles_profiles/examples/common.yaml /var/lib/hiera -> if you have install the module.

$ cp ../galaxy_roles_profiles/examples/common.yaml /var/lib/hiera -> if you use the repo from GitHub directly.

More details on Hiera at : http://docs.puppetlabs.com/hiera/1/

More details on automatic parameter lookup :  http://docs.puppetlabs.com/hiera/1/puppet.html#automatic-parameter-lookup

##Github projects
Projects for base blocks and roles+profiles are hosted on github:


https://github.com/puppet-galaxy/puppet-galaxy


https://github.com/puppet-galaxy/galaxy-roles-profiles

##Contact

Mikael Loaec    mloaec@versailles.inra.fr


Olivier Inizan  oinizan@versailles.inra.fr


Eric Rasche     rasche.eric@yandex.ru

##Galaxy Project
http://galaxyproject.org
