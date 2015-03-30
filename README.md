Erlang [![Build Status](https://travis-ci.org/mtpereira/ansible-erlang.svg)](https://travis-ci.org/mtpereira/ansible-erlang)
=========

Installs Erlang from a custom repository. By default it'll install the latest ```erlang``` and ```erlang-manpages``` packages available from [Erlang Solutions repositories](https://packages.erlang-solutions.com/erlang/).

Requirements
------------

None.

Role Variables
--------------

Required variables:

* `erlang_packages_state`: State for `apt` module, for defining if packages should be installed, upgraded to latest version or removed. Default to `latest`.
* `erlang_additional_packages`: List of additional packages to install. Defaults to `[erlang-manpages]`.
* `erlang_repo`: Repository URL for package installation. Defaults to `http://packages.erlang-solutions/` for Debian and to `https://packages.erlang-solutions.com/` for Ubuntu.
* `erlang_repo_key_url`: GPG key URL for repository validation. Defaults to `https://packages.erlang-solutions.com/{{ ansible_distribution | lower }}/erlang_solutions.asc`.
* `erlang_repo_key_server`: GPG key server URL for repository validation. Used in conjunction with `erlang_repo_key_id`. If these two variables are defined, do not define `erlang_repo_key_url`.
* `erlang_repo_key_id`: GPG key ID for repository validation. Used in conjunction with `erlang_repo_key_server`. If these two variables are defined, do not define `erlang_repo_key_url`.
* `erlang_pin`: Defines if the `erlang_repo` will be [pinned](https://wiki.debian.org/AptPreferences#Pinning). Defaults to `true`.

Internal variables, avoid changing:

* `erlang_packages_force`: Forces package installation when packages are not authenticated. This is happening on Erlang-Solution's Debian repository. Defaults to `yes` for Debian and `no` for every other distribution.
* `erlang_pin_priority`: Pin priority. Defaults to `999`, so that the `erlang_repo` as priority over other repositories except when it would downgrade the installed package.

Dependencies
------------

None.


Testing
-------

Tests can be ran on Debian Wheezy and Ubuntu Trusty boxes by executing "vagrant up".

Example Playbook
----------------

    - hosts: servers
      roles:
         - mtpereira.erlang
           erlang_additional_packages:
             - erlang-doc
             - erlang-manpages
             - erlang-mode
           sudo: yes

License
-------

BSD

Author Information
------------------

Thanks to [Erlang Solutions](https://www.erlang-solutions.com/) for the Erlang packages repository.

[GitHub project page](https://github.com/mtpereira/ansible-ruby)

[Manuel Tiago Pereira](http://mtpereira.github.io)
