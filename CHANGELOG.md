#2014-07-0.8 Release 1.0.0

=> Include galaxy::directories in common.pp to fixes somes bug at the initial run.

#2014-31-07 Release 0.0.9
=> Common returns. It downloads galaxy and create an user, a directory and manages config files.

=>Roles : galaxy-sqlite, galaxy-postgresql , galaxy-apache-sqlite, galaxy-apache-postgresql
 And the configuration of onecore or multicore is now done by Hiera

=>Profiles : each profiles are one service except profile ::common.

=>All configuration can be done through Hiera and a file.yaml

=> Removed profile ::base


#2014-08-07 Release 0.0.8

=> Common does not exist anymore

=> Add role onecore database

=> Add profile onecore-database, multicore-database , multicore , onecore  : These manage universe.ini and other config files. Onecore launch galaxy as a service.

=> Resolve minor bug when we add one database like postgresql.


#2014-26-06 Release 0.0.7

=> Multicore OK.

Known issue:

With VM wich does not have enough resources, if you want to use multicore,

the first time you run GALAXY_RUN_ALL=1 ./run.sh --daemon, one web could not run correctly.

In that case, simply re-run the command GALAXY_RUN_ALL=1 ./run.sh --daemon.

Or GALAXY_RUN_ALL=1 ./run.sh --stop-daemon and then GALAXY_RUN_ALL=1 ./run.sh --daemon.


=> When Galaxy is running , there is not login required anymore.

#2014-26-06 Release 0.0.6

=> Corrections for webapp. rewrite_rule is now set correctly with an array of arguments.
