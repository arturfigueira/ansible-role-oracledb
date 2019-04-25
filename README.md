# Oracle DB
Install and configure Oracle Database 11g Release 2 on a RHEL/CentOs 6.x

## Dependences
Oracle 11G installer, which is composed of two zip files, should be downloaded priorhand and placed
on a directory of the installation's server. Case you are using Vagrant the installers
can be placed on a sync folder on the host machine (Beware for this approach, case oracle_auto_start variable is **TRUE**, ansible will remove all zip files from the **host**)

Oracle 11g Release 2 can be found at [Oracle Database Donwloads] (https://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html)

## Notes
The installation process is using pre install packages from Oracle (aka oracle-rdbms-server-11gR2-preinstall), which automatically configures the server with required settings and packages, this includes the creation of users and groups. For this reason this role will **ALWAYS** installs oracle database under *oracle* user and *oinstall* group.

## Variables
```yml
#Install folder
oracle_installers_dir: Folder with required zip files to install Oracle DB
oracle_db_home: Oracle Home folder: Default: db_1
oracle_base_dir: Default: /u01/app
oracle_product_dir: Default: product/11.2.0
oracle_install_dir: Oracle full installation path: Default: "{{ oracle_base_dir }}/oracle/{{ oracle_product_dir }}/{{ oracle_db_home }}"

#Database settings
oracle_sid: Database Default SID. Default: DB11G
oracle_listener_port: Oracle Listener Port. Default: 1521
oracle_db_oper_group: DBA group name. Default: dba
oracle_db_syspwd: System User default password
oracle_db_mem: Total memory allocated to Oracle
oracle_auto_start: Enable oracle service to install automatically. Values: true | false. Default: true
oracle_cleanup_install: Remove all responseFiles and installation files from the server. Values: true | false. Default: true
```

## Playbook
```yml
- name: Install and Configure Oracle
  hosts: all
  become: yes
  roles:
    - role: oracle
      vars:
        oracle_sid: XE
        oracle_db_home: xe
        oracle_installers_dir: /tmp/oracle
        oracle_auto_start: false
```

## Compatibility

* [Ansible 2.+](https://www.ansible.com/)
* [CentOS 6 / 7](https://www.centos.org/)
* [Oracle Database 11gR2](https://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html)

## Contributing
Please read [CONTRIBUTING.md]([CONTRIBUTING.md]) for details on our code of conduct, and the process for submitting pull requests to me.

## Versioning
We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository]().

## Authors
*  [ArturFigueira](https://github.com/arturfigueira) - *Initial work*

## License
This project is licensed under the GNU GENERAL PUBLIC LICENSE - see the [LICENSE.md](LICENSE.md) file for details.
