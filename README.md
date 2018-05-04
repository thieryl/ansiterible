ansible-magento
===========================

| date:     |  04 May 2018  |
|----------|---|
| tags:     | cloud, magento  |
| category: | Amazon Linux  |


## Provision Cloud Server with Magento/Nginx/PHP-FPM/Varnish & MySQL
####Usage:

Edit `group_vars/all` to define: hostname, domain, users etc.

Explanation for each variable:

magento_version: 1.8.1.0 <== this one is pretty much self-explanatory <br />
magento_db_name: <== database used for the Magento installation <br />
magento_db_user: <== database user used for the Magento installation <br />
magento_db_password: <== password for user <br />
magento_db_remote_host: <== the eth1 IP address of the web server <br />
mysql_port: <== used to install Magento together with the `magento_db_remote_host, magento_db_rpassword, magento_db_user, magento_db_name` <br />
mysql_host: <==
server_hostname: <== used for Nginx/PHP-FPM/Varnish config <br />
mysql_root_password: <== new password for mysq root user (this needs to be changed on roles/mysql/templates/root.my) <br />
magento_admin_first: <== admin user for the magento website <br />
magento_admin_last:  <== details <br />
magento_admin_email: <== email address used for the admin user <br />
magento_admin_user:  <== user <br />
magento_admin_pass:  <== password <br />
magento_domain: <== the magento installation domain
php_listen: <== PHP-FPM should use sockets or TCP (defaults on sock)


---
####ToDo:

* Better documentation
* Multiple web nodes
* Build the servers too

# ansible-newrelic

This ansible role installs and configures the New Relic Server Agent (System Monitor Daemon)

## Requirements

This role requires Ansible 1.4 higher and platforms listed in the metadata file.

## Role Variables

The variables that can be passed to this role and a brief description about them are as follows

    # License key
    newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16

    # Log level (error, warning, info, verbose, debug, verbosedebug)
    newrelic_loglevel: info

    # Log file location
    newrelic_logfile: /var/log/newrelic/nrsysmond.log

    # Proxy server. Default False
    newrelic_proxy: fred:secret@proxy.mydomain.com:8181

    # Use SSL for all communication. Default False
    newrelic_ssl: "true"

    # SSL CA Bundle path. Default False
    newrelic_ssl_ca_bundle: /etc/pki/tls/certs/ca-bundle.crt

    # SSL CA Path. Default False
    newrelic_ssl_ca_path: /etc/ssl/certs

    # Pid file locaiton
    newrelic_pidfile: /var/run/newrelic/nrsysmond.pid

    # Collector hostname
    newrelic_collector_host: collector.newrelic.com

    # Connection timeout for collector host
    newrelic_timeout: 30

## Examples

### Paramaterized Role

    ---
    - hosts: all
      roles:
        - { role: newrelic, newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16 }

### Vars

    ---
    - hosts: all
      vars:
        newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16
      roles:
        - newrelic

### Group vars

#### group_vars/production

    ---
    newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16
