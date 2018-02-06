# localdev
Local development environment, built with Vagrant and configured with Ansible.

(Work in progress)

# Includes
* Multi-platform (Ubuntu 16.04 / CentOS 7)
* Software options:
    * Common (required)
        * Useful bash and git customizations
    * Python
        * Supports both Python 2 and Python 3
        * Virtual environments
    * Apache 2.4
    * PHP 7.2
    * MariaDB
    * phpMyAdmin

* Use it as a starting point for your environment. Include other packages you want.
* To do:
    * JavaScript
    * Ruby
    * Java
    * Refine Apache installation.

# Instructions
* Select OS in the `vagrantfile`.
* Place your private key (for Git checkouts) at `~/.ssh/id_rsa`.
* Enter user variables in `roles/common/vars/user.yml`.
* Choose software to be installed in `site.yml`. Comment out the roles to skip.