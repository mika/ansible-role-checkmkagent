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
# The packaged agents can be found on the check_mk server.
# The deb file can be found in '/check_mk/agents/check-mk-agent_$check_mk_version-1_all.deb'
# und the 'checkmkagent_agent_baseurl'
# checkmkagent_agent_baseurl: 'http://monitor01.example.com/$site'
```

Dependencies
------------

N/A

Example Playbook
----------------

```
    - hosts: site
      var:
        checkmkagent_agent_baseurl: 'http://monitor01.example.com/mysite'
      roles:
         - { role: jkirk.checkmkagent }
```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
