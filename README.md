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

# The packaged agents can be found on the check_mk server.
# The deb file can be found in '/check_mk/agents/check-mk-agent_{{ checkmkagent_version }}-1_all.deb'
# under the 'checkmkagent_baseurl'
```

Dependencies
------------

N/A

Example Playbook
----------------

```
    - hosts: site
      var:
        checkmkagent_baseurl: 'http://monitor01.example.com/mysite'
      roles:
         - { role: jkirk.checkmkagent }
```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
