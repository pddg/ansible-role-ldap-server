Role Name
=========

Ubuntuにslapdをインストールしてユーザを作成する

Requirements
------------

対象ホストの`/etc/hosts`を正しく編集しておく．testsディレクトリ以下を参照．

Role Variables
--------------

[defaults.yml](./defaults/main.yml)を見る

Dependencies
------------

無し

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
    - name: pddg.ldap_server
      vars:
        ldap_server_domain: example.com
        ldap_server_passwd: password
        ldap_server_user_entries:
          example-user:
            cn: Example User
            sn: User
            givenName: Example
            uidNumber: 1000
            gidNumber: 1000
        ldap_server_group_entries:
          admin:
            gidNumber: 10
            memberUid:
              - example-user
```

License
-------

MIT

Author Information
------------------

[pddg](https://github.com/pddg/)
  - Web: [poyo.info](https://www.poyo.info/)

