checkmkagent
============

A simple role to deploy the Check_Mk Agent with some custom local checks and plugins.

Requirements
------------

N/A

Role Variables
--------------

Taken from [defaults/main.yml](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/defaults/main.yml):
```yaml
# Set the version of the Check_Mk server
checkmkagent_version: '1.5.0p21'

# The agent package can be found on the check_mk server,
# the deb file will be downloaded from '{{ checkmkagent_host_url }}/check_mk/agents/check-mk-agent_{{ checkmkagent_version }}-1_all.deb'
# If not defined, the agent will not be installed.
# checkmkagent_host_url: 'http://monitor01.example.com/mysite'

# Some plugins should only be deployed if explicitly requested.
# See files/check-mk/plugins for the list of currently supported plugins
# (The Agent Plugin mk_apt will be deployed automatically if the OS 'debian' is detected)
# checkmkagent_plugins: [ '' ]
```

Local checks and plugins
------------------------

See:

* [files/check-mk/local](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/files/check-mk/local)
* [files/check-mk/plugins](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/files/check-mk/plugins)

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
% ansible -i hosts all -b -m shell -a "rm /usr/lib/check_mk_agent/plugins/60"

```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
