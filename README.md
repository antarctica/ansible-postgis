# PostGIS (`postgis`)

**Part of the BAS Ansible Role Collection (BARC)**

Installs the PostGIS PostgreSQL extension and optionally enables this within an 'app' db

## Overview

* Installs the PostGIS PostgreSQL extension.
* Where this role is used with the `postgresql-server` role the PostGIS extension will be automatically enabled within the app database, if the `postgresql-server` uses this.

## Availability

This role is designed for internal use but if useful can be shared publicly.

## Usage

### Requirements

#### BAS Ansible Role Collection (BARC)

* `postgresql-server`

#### Other

* Due to the package name used by PostGIS this role installs a specific version of PostGIS for a specific version of PostgreSQL. You **MUST** ensure you have the specified version of PostgreSQL installed for installation of this role to occur. This is a known issue and will be looked into. The current required software versions are:
    * PostGIS: 2.1 (installed as part of this role)
    * PostgreSQL: 9.3

### Variables

* `postgis_controller_postgresql_user_username`
    * The username of the PostgreSQL user to enable the PostGIS extension within databases
    * This variable **MUST** be a valid PostSQL user and this user **MUST** have suitable permissions to enable extensions within databases.
    * By default, this variable will use the `postgresql_server_controller_postgresql_user_username` variable if available. If not, a fall back value will be used.
    * Default: "{{ postgresql_server_controller_postgresql_user_username }}" if defined otherwise, "controller"
* `postgis_controller_postgresql_user_password`
    * Password for PostgreSQL controller user.
    * This variable **MUST NOT** contain ":" characters to ensure compatibility with `.pgpass` files
    * By default, this variable will use the `postgresql_server_controller_postgresql_user_password` variable if available. If not, a fall back value will be used.
    * Default: "{{ postgresql_server_controller_postgresql_user_password }}" if defined otherwise, "stirring-up^the=flames$381194££iz€JQ4"
* `postgis_app_db_name`
    * The name of the 'app' database in which PostGIS should be enabled, if used
    * This variable **MUST** be a valid PostgreSQL database and the user identified by `postgis_controller_postgresql_user_username` **MUST** have permissions to enable extensions within this database.
    * By default, this variable will use the `postgis_app_db_name` variable if available. If not, a fall back value will be used.
    * Default: "{{ postgis_app_db_name }}" if defined otherwise, "app"
* `postgis_enable_app_db`
    * If "true" the PostGIS extension will be enabled within the database identified by `postgis_app_db_name`
    * By default, this variable will use the `postgis_enable_app_db` variable if available. If not, a fall back value will be used.
    * Default: "{{ postgis_enable_app_db }}" if defined otherwise, "false"

## Contributing

This project welcomes contributions, see `CONTRIBUTING` for our general policy.

## Developing

### Committing changes

The [Git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow/) workflow is used to manage development of this package.

Discrete changes should be made within *feature* branches, created from and merged back into *develop* (where small one-line changes may be made directly).

When ready to release a set of features/changes create a *release* branch from *develop*, update documentation as required and merge into *master* with a tagged, [semantic version](http://semver.org/) (e.g. `v1.2.3`).

After releases the *master* branch should be merged with *develop* to restart the process. High impact bugs can be addressed in *hotfix* branches, created from and merged into *master* directly (and then into *develop*).

### Issue tracking

Issues, bugs, improvements, questions, suggestions and other tasks related to this package are managed through the BAS Web & Applications Team Jira project ([BASWEB](https://jira.ceh.ac.uk/browse/BASWEB)).

## License

Copyright 2015 NERC BAS. Licensed under the MIT license, see `LICENSE` for details.
