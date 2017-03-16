# Ansible Role: Terminator

Install and configure Terminator terminal: <https://launchpad.net/terminator>

## Requirements

- Ansible >= 2.2
- Fedora 25
- sudo

The role may run on other systems, but it is not tested.

## Role Variables

Deploy and overwrite the Terminator configuration file (true | false).

```
terminator_overwrite_config: true
```

Terminator configuration template file. The default have my personal preferences.

```
terminator_template: templates/config.j
```

User list that will deploy the configuration. The default will get the ansible user.

```
terminator_users:
  - {
      name: "{{ ansible_user_id }}",
      home: "{{ ansible_user_dir }}",
    }
```

## Example

### Simple

```
- hosts: all
  roles:
    - ansible-role-terminator
```

### With custom variables

File structure:

```
roles/ansible-role-terminator/**
templates/custom_terminator_conf.j2
my_playbook.yml
hosts
```

`my_playbook.yml`:

```
- hosts: all
  roles:
    - ansible-role-terminator
    vars:
      terminator_overwrite_config: true
      terminator_template: ./templates/custom_terminator_conf.j2
      terminator_users:
        - {
            name: USERNAME,
            home: /home/USERNAME,
          }
        - {
            name: root,
            home: /root,
          }
```

`hosts`:

```
[all]
localhost ansible_connection=local
```

`custom_terminator_conf.j2`:

```
see: https://github.com/tovletoglou/ansible-role-terminator/templates/config.j2
```

## Dependencies

None

## License

MIT

## Author Information

Apostolos Tovletoglou [ansible-role-terminator](https://github.com/tovletoglou/ansible-role-terminator)
