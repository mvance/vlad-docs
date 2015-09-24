<h1>Variables</h1>

The following variables can be set in Vlad's [settings file](settings_file.md).

## Webserver

__webserver_hostname__

The hostname of the site you are about to create. By default this is then combined with the variable webserver_hostname_alias to add 'www' to the start.

default value: 'drupal.local'

__webserver_hostname_aliases__

In order to support multiple projects, or Drupal multi-site installations, this lets you add a list of fully qualified names for your web server aliases.

default value:
- 'www.drupal.local'

## Vagrantfile configuration

__boxipaddress__

The IP address of the virtual machine.

default value: "192.168.100.100"

__boxname__

The name of the box that will be used by Vagrant to label the box inside your virtual machine manager of choice. This value should only contain letters, numbers, hyphens or dots. The VM will appear as `boxname` + "_vlad" in your chosen virtual machine manager.

default value: "vlad"

__vlad_os__

The OS that vlad will use. This can be one of the following:

- "centos65"
- "ubuntu12"
- "ubuntu14"

default value: "ubuntu14"

__host_synced_folder__

This is the directory that will be used to server the files from. If this doesn't exist then it will be created.

default value: "./docroot"

__aux_synced_folder__

This is a secondary Vagrant synced folder used to sync files that don't belong in `host_synced_folder`. If this doesn't exist then it will be created.

default value: "./vlad_aux"

__synced_folder_type__

*Only applicable for when running Vlad on a non-Windows host.*
Use 'nfs' or 'rsync' for VM file editing in synced folder.

default value: 'nfs'

__ansible_verbosity__

Set the level of verbosity that Ansible will use.
This can be one of "", "v", "vv", "vvv", or "vvvv".

default value: ""

__vm_cpus__

Number of CPU cores to be allocated to the guest VM from the host machine. This can be an integer or can be set to `"auto"` for Vlad to automatically assign all available cores.

default value: '2'

__vm_memory__

Amount of memory to be allocated to the guest VM from the host machine. This can be an integer (MB) or can be set to `"auto"` for Vlad to automatically assign 1/4 of host machine's memory.

default value: '1024'

__parallels_update_guest_tools__

Whether the `vagrant-parallels` plugin should update the Guest Tools in the VM automatically.

default value: false

__vlad_custom_base_box_name__

This sets the custom base box for Vlad to use when utilizing the custom base box functionality. This requires a custom base box to be setup or provided. [Please read the documentation on setting up the custom base box if you want to use this feature](custom_box.md).

default value: ""

## Components to install

The server components that will be installed when the box is provisioned.

- To install a component set it to true.
- To leave a component out of the install set the value to false.

__adminer_install__

Installs Adminer.

default value: true

__apache_install__

Installs Apache server.

default value: true

__bling_install__

Adds bling.

default value: true

__imagemagick_install__

Installs Imagemagick as well as the PHP extension.

default value: false

__mailcatcher_install__

Installs Mailcatcher. Also installs the Ruby task as a dependency.

default value: false

__memcached_install__

Installs Memcache as well as the PHP extension.

default value: false

__munin_install__

Installs Munin server.

default value: false

__mysql_install__

Installs MySQL.

default value: true

__node_install__

Installs Node.

default value: false

__php_install__

Installs PHP, including a number of PHP packages as well as APC, Composer, and Xdebug.

default value: true

__pimpmylog_install__

Installs PimpMyLog.

default value: false

__redis_install__

Installs Redis.

default value: false

__ruby_install__

Installs Ruby. Ruby is required by MailCatcher.

default value: false

__sendmail_install__

Installs the Sendmail server.

default value: false

__solr_install__

Installs Tomcat 6 and Solr 4.

default value: false

__varnish_install__

Installs Varnish. Vlad will run checks to ensure that varnish can listen on port 80 and that Apache doesn't clash with that port.

default value: false

__xhprof_install__

Installs Xhprof and a Xhprof GUI.

default value: false

## Custom playbook

Vlad provides the following variables to help you integrate a custom playbook as part of provisioning.

| Variable | Type | Default value | Description |
|---|---|---|---|
| `vlad_custom_play` | Boolean | false | Determines whether the custom playbook will run when Vlad provisions the VM. |
| `vlad_custom_play_path` | String  | "../vlad_custom/" | Relative path to the directory that contains the custom playbook (relative to Vlad's Vagrantfile). Note the closing backslash. |
| `vlad_custom_playfile`  | String | "provision.yml" | Name of the YAML file to run within the custom playbook (including extension). |

See [Custom playbook](../usage/custom_playbook.md) for more information.

## HTTP ports

__http_port__

HTTP port for the web server. If you have opted to install Varnish you will likely want to change this to `8080`.

default value: 80

__varnish_http_port__

HTTP port for the Varnish cache.

default value: 80

## Administration email

__admin_mail__

Used in instances when a server email is needed.

default value: 'test@example.com'

## PHP

__php_version__

The version of PHP to install (dependent on OS). Can be one of:

- "5.3"
- "5.4"
- "5.5"
- "5.6"

Note that Ubuntu 14 won't install < PHP5.4 so you'll get PHP5.5+. Vlad will error when a version that isn't understood is used.

default value: "5.5"

### php.ini

__php_memory_limit__

default value: 512M

__php_max_execution_time__

default value: 60

__php_post_max_size__

default value: 100M

__php_upload_max_filesize__

default value: 100M

__php_display_errors__

default value: On

__php_display_startup_errors__

default value: On

__php_html_errors__

default value: On

__php_date_timezone__

default value: Europe/London

### Install PECL uploadprogress

__php_pecl_uploadprogress__

default value: false

### PHP APC

__apc_rfc1867__

default value: '1'

__apc_shm_size__

default value: '256M'

__apc_shm_segments__

default value: '1'

__apc_num_files_hint__

default value: '0'

## MySQL

__mysql_port__

default value: 3306

__mysql_root_password__

default value: sdfds87643y5thgfd

__server_hostname__

default value: vlad

__dbname__

This is a list of databases that Vlad will generate. As a default a single database is created but this value can be changed to make Vlad add more databases. The following setting will generate two databases, one called 'database1' and the other called 'database2'.

    dbname: ['database1', 'database2']

Each database has the same access privileges.

It should be noted that the first database in this list is always used as the default database. This database is used by Vlad when running automatic actions such as exporting or importing the database.

default value: ['vladdb']

__dbuser__

The user that will be created for the databases.

default value: vlad

__dbpass__

The password for the database user.

default value: wibble

__db_import_up__

Import MySQL databases from files on 'vagrant up'.

Database import won't occur if the first present database has any tables defined (in order to prevent data loss).

Options include:

- `false` - don't import anything
- `true` - import from files within vlad_aux/db_io/halt_destroy/ - source filenames will need to correspond with values in `dbname`.
- `["path_to_file","path_to_file"]` - import from vlad_aux/db_io/[path_to_file]. Requires an entry for each database specified in `dbname`. Supports .sql, .bz2 and .gz files.

default value: false

### MySQL my.cnf

__mysql_max_allowed_packet__

default value: 128M

__innodb_buffer_pool_size__

default value: 64M

__innodb_file_per_table__

default value: true

__innodb_log_file_size__

default value: 64M

__mysql_character_set_server__

default value: utf8

__mysql_collation_server__

default value: utf8_general_ci

__skip_name_resolve__

default value: true

__mysql_hosts__

A list of hosts that MySQL should map to databases to allow access.

default value: ['{{ local_ipv4_address.ansible_facts.ansible_default_ipv4.address }}', '127.0.0.1', 'localhost']

__mysql_allow_all_hosts__

Whether to allow all hosts (0.0.0.0) or a specific IP address (which is taken from the boxipaddress variable)
default value: true

__mysql_slow_query_log_status__

This sets the MySQL slow query log status. Turn on with 1, turn off with 0.

default value : 0

__mysql_slow_query_log_location__

This sets the location of the MySQL slow query log.

default value : '/var/log/mysql/mysql-slow.log'

__mysqL_long_query_time__

The amount of time that a query must last before being logged into the slow query log.

default value: 2

mysql_log_queries_not_using_indexes

Whether MySQL should also log any query that doesn't use indexes.

default value: false

## SSH

__ssh_port__

default value: 22

__use_host_id__

Add RSA or DSA identity from host to guest on 'vagrant up'.
Does not support identities that require a passphrase.

Options include:

- false         : don't add anything
- true          : add default files  (~/.ssh/id_rsa, ~/.ssh/id_dsa & ~/.ssh/identity)
- "[filename]"  : add a specific file e.g. /Users/username/.ssh/[filename]

NOTE: In order for this to work correctly you also need to setup agent forwarding on your host machine. This is done by including the following into your ~/.ssh/config file. This assumes that you are keeping the default '.local' domains that come with Vlad.

    Host *.local
        ForwardAgent yes

default value: false

## Varnish

__varnish_memory__

Sets the amount of memory that Varnish can use (in Megabytes).

default value: 512

## Redis

__redis_port__

Sets the port Redis should listen on.

default value: 6379

## Drush make

__drush_make_file__

The name of the make file that is to be run. Vlad expects this file to be placed in a subdirectory called "make" within your vlad_aux directory.

E.g. "vlad_example_d7.make"

Drush make will not be run if no file is specified.

default value: ""

__drush_make_options__

Options to pass to drush make command.

E.g. "--prepare-install"

See http://www.drushcommands.com/drush-6x/make/make for possible options.

default value: ""

__drush_make_force__

Run drush make *every* time the VM is provisioned. Setting to false will only run drush make if a make file has been specified and docroot does not contain an existing Drupal codebase.

default value: false

__drush_structure_tables__

Sets the tables to be skipped in the "$options['structure-tables']['common']" config variable in the .drushrc.php file. Allows you to run drush database dump commands using the --structure-tables-key parameter to skip certain table data like caches and session data. For example, to export the database and skip those tables you would run the following command.

    drush sql-dump --structure-tables-key=common --gzip --result-file=dump.sql

default value: "['cache','cache_filter','cache_menu','cache_page','history','sessions','watchdog','cache_admin_menu','cache_block','cache_field','cache_form','cache_path','cache_token','cache_update','cache_views','cache_views_data','ctools_css_cache','ctools_object_cache','search_dataset','search_index','search_node_links','search_total']"

## Bling

__bling_shell_prompt__

Tweaks shell prompt.

default value: true

## Other settings

__drupal_solr_package__

Select which Solr module to install accepted values are 'search_api_solr' or 'apachesolr'

default value: "search_api_solr"

__hosts_file_location__

Local hosts file location.

Default location on *nix hosts is '/etc/hosts'.

Default location for GasMask on OSX is '/Users/< username >/Library/Gas Mask/Local/< file >.hst'.

default value: "/etc/hosts"

__hosts_file_update__

Select whether Vlad should edit the hosts file.

default value: true

__add_index_file__

Add the default index.php file (useful to turn off if you are going git clone into the web root folder). Vlad will also not overwrite any existing index.php file present in the docroot location.

default value: true

__drush_aliases_assemble__

Drush alias files can be placed in either of Vlad's settings directories. See http://vlad-docs.readthedocs.org/en/latest/usage/settings_file

Setting to true will assemble all alias/aliases files into a single group aliases file prefixed with the boxname.

Setting to false will copy alias/aliases files to the guest without assembling or renaming.

default value: false

## Git config user credentials

Leave these variables empty to skip this step.

__git_user_name__

Your git username.

default value: ""

__git_user_email__

Your git email address.

default value: ""
