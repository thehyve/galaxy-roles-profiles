#Galaxy roles profiles
####Tables of Contents
1. [Overview](#overview)
2. [Module Description](#module-description)
3. [Setup](#setup)
    * [First step with Puppet Galaxy](#first-step)
4. [Available Roles for quick start](#roles)
    * [Role galaxy-roles-profiles::role::basic](#role-basic)
    * [Role galaxy-roles-profiles::role::multicore](#role-multicore)
    * [Role galaxy-roles-profiles::role::multicore-database](#role-multicore-database)
5. [Profiles](#profiles)
    * [Profile galaxy-roles-profiles::profile::base](#profile-base)
    * [Profile galaxy-roles-profiles::profile::common](#profile-common)
    * [Profile galaxy-roles-profiles::profile::database](#profile-database)
    * [Profile galaxy-roles-profiles::profile::webapp](#profile-webapp)
6. [Deal with Hiera configuration files](#hiera)   
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

```puppet
	include galaxy-roles-profiles::role::<the role wich you want>
```
##Roles 
Roles contains only one or many profiles.
 
###Role basic
Galaxy in basic config. It means with SQLite and only one core.

```puppet
	include galaxy-roles-profiles::role::basic
```

###Role multicore
Galaxy in load-balancing mode with SQLite.

```puppet
	include galaxy-roles-profiles::role::multicore
```
###Role multicore-database
Galaxy in load-balancing mode with PostgreSQL.

```puppet
	include galaxy-roles-profiles::role::multicore-database
```

##Profiles
Profiles contains one or many building-block (for example galaxy::universe). One profile is one technology layer.

###Profile base
This profile install Galaxy and make the first run of Galaxy

###Profile common
This profile manage toolshed_conf, job_conf and universe_wsgi.ini. Actually each configuration is written right here with if and elsif statement.
This profile is parametrable: $config for choose wich config you want ( onecore | multicore | multicore-database).
There are lot of parameters set by Hiera wich are used in galaxy::universe ( see 6.Hiera and https://github.com/puppet-galaxy/puppet-galaxy).
In the future, each configuration ( one config = one universe ) will be separated from this profile.

###Profile database
This profile install packages for postgresql, and configure it for add a new database for galaxy.
This uses the puppetlabs/postgresql module.
It's a very basic use of the postgresql module : create an user, a password and a database.
These are set in a Hiera file. ( see 6.Hiera ).
Further information available at : https://forge.puppetlabs.com/puppetlabs/postgresql .

###Profile webapp
This profile install and configure apache to deal with Galaxy in load-balancing mode.
This uses puppetlabs/apache module to install apache, create a Virtual Host and load the needed mods
To deal with balancer configuration file, we write a template ( balancer_galaxy.conf.erb ) and a class `galaxy-roles-profiles::balancer-config`
Further information available at : https://forge.puppetlabs.com/puppetlabs/apache .


##Hiera
First you have to edit the hiera.yaml in /etc/hiera.yaml and in /etc/puppet/hiera.yaml (for example delete each lines in hierarchy and add "common" ).

Next you have to have one hiera file in /var/lib/hiera/ ( for example common.yaml) 

You can use a sample of common.yaml and modify it as you want :

$ cp /etc/puppet/modules/galaxy_roles_profiles/examples/common.yaml /var/lib/hiera -> if you have install the module.

$ cp ../galaxy_roles_profiles/examples/common.yaml /var/lib/hiera -> if you use the repo from GitHub directly.

More details on Hiera at : http://docs.puppetlabs.com/hiera/1/

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
