# checkmkagent

![Lint Code Base](https://github.com/jkirk/ansible-role-checkmkagent/actions/workflows/superlinter.yml/badge.svg)

A simple role to deploy the checkmk agent with some custom local checks and agent plugins.

## Requirements

N/A

## Role Variables

See: [defaults/main.yml](https://github.com/jkirk/ansible-role-checkmkagent/tree/master/defaults/main.yml)

## Local checks

Currently the following local checks are deployed default:

* `check_kernel_freshness`
* `check_storagebox`

The local megacli checks are not deployed automatically:

* `check_megacli_battery`
* `check_megacli_diskgroups`
* `check_megacli_firmware`
* `check_megacli_num_disks`
* `check_megacli_smart`

To do so the following role variables need to be defined:

* `checkmkagent_megacli_num_disks`
* `checkmkagent_megacli_num_disk_groups`
* (optionall and agent pluginsy) `checkmkagent_megacli_battery_adapter`

## Agent plugins

Currently the following checkmk agent plugins are supported:

```yaml
checkmkagent_plugins_available: [ 'mk_ceph', 'mk_logwatch.py', 'mk_mysql' ]
```

For general available agent plugins see the agent plugins folder of your checkmk monitoring server (i.e. `https://monitoring.example.com/mysite/check_mk/agents/plugins/`).

## Dependencies

N/A

## Example Playbook

```yaml
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

## Update / Migration Notes

### xinetd -> systemd migration

To migrate to systemd, checkmk 2.2+ needs to be installed.

To keep the xinetd integration for hosts which do not have checkmk 2.2+ and
still have xinetd installed and configured `checkmkagent_service_xinetd: true`
needs to be set.

Note, no xinetd configuration is deployed anymore, even if
`checkmkagent_service_xinetd: True` is set.

### mk_apt

`mk_apt` was installed in `/usr/lib/check_mk_agent/plugins/60` instead of `/usr/lib/check_mk_agent/plugins/3600`.
To delete the check on all hosts from the wrong location you could use ansible like this:

```console
% ansible -i hosts all -m shell -a "ls -l /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i hosts all -b -m shell -a "rm /usr/lib/check_mk_agent/plugins/60/mk_apt"
% ansible -i hosts all -b -m shell -a "rmdir /usr/lib/check_mk_agent/plugins/60"

```

### Variable names

Older versions of this role used the variable `checkmkagent_baseurl` instead `checkmkagent_host_url`.

## License

MIT

## Author Information

Darshaka Pathirana - <https://synpro.solutions>
