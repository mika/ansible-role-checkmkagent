checkmkagent
============

A simple role to deploy the checkmk agent with some custom local checks and agent plugins.

Requirements
------------

N/A

Role Variables
--------------

See: [defaults/main.yml](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/defaults/main.yml)

Local checks and agent plugins
------------------------------

For currently available local checks, see: [files/check-mk/local](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/files/check-mk/local).

Currently the following checkmk agent plugins are supported:

```
checkmkagent_plugins_available: [ 'mk_ceph', 'mk_logwatch.py', 'mk_mysql' ]
```

For general available agent plugins see the agent plugins folder of your checkmk monitoring server (i.e. `https://monitoring.example.com/mysite/check_mk/agents/plugins/`).

Dependencies
------------

N/A

Example Playbook
----------------

```
    - hosts: site
      vars:
        checkmkagent_host_url: 'http://monitor01.example.com/mysite'
      roles:
         - { role: jkirk.checkmkagent }

    - hosts: ceph
      roles:
         - role: jkirk.checkmkagent
           checkmkagent_host_url: 'http://monitor01.example.com/mysite'
           checkmkagent_plugins: [ 'mk_ceph' ]
```

Update Notes
------------

Older versions of this role used the variable `checkmkagent_baseurl` instead `checkmkagent_host_url`.

`mk_apt` was installed in `/usr/lib/check_mk_agent/plugins/60` instead of `/usr/lib/check_mk_agent/plugins/3600`.
To delete the check on all hosts from the wrong location you could use ansible like this:

```
% ansible -i hosts all -m shell -a "ls -l /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i hosts all -b -m shell -a "rm /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i hosts all -b -m shell -a "rmdir /usr/lib/check_mk_agent/plugins/60"

```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
