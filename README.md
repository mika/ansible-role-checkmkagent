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

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
