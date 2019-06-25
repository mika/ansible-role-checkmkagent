checkmkagent
============

A simple role to deploy the Check_Mk Agent.

Requirements
------------

N/A

Role Variables
--------------

Take from `defaults/main.yml`:
```yaml
# Set the version of the Check_Mk server
# checkmkagent_version: '1.5.0p14'

# The agent package can be found on the check_mk server,
# the deb file will be downloaded from '{{ checkmkagent_host_url }}/check_mk/agents/check-mk-agent_{{ checkmkagent_version }}-1_all.deb'
# If not defined, the agent will not be installed.
# checkmkagent_host_url: 'http://monitor01.example.com/mysite'
```

Dependencies
------------

N/A

Example Playbook
----------------

```
    - hosts: site
      var:
        checkmkagent_host_url: 'http://monitor01.example.com/mysite'
      roles:
         - { role: jkirk.checkmkagent }

    - hosts: debian
      var:
      roles:
         - role: jkirk.checkmkagent
           checkmkagent_host_url: 'http://monitor01.example.com/mysite'
           checkmkagent_plugins: [ 'mk_apt' ]

    - hosts: ceph
      var:
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
% ansible -i rfid.hosts all -m shell -a "ls -l /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i rfid.hosts all -b -m shell -a "rm /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i rfid.hosts all -b -m shell -a "rm /usr/lib/check_mk_agent/plugins/60"

```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
