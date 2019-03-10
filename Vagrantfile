# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    require 'json'
    ldap_server_user_entries = {
        "t-kosen": {
            "cn": "Taro Kosen",
            "sn": "Kosen",
            "givenName": "Taro",
            "uidNumber": 2000
        },
        "h-kosen": {
            "cn": "Hanako Kosen",
            "sn": "Kosen",
            "givenName": "Hanako",
            "gidNumber": 999,
            "uidNumber": 2001
        }
    }
    ldap_server_group_entries = {
        "groupA": {
            "gidNumber": 100,
            "memberUid": [
                "t-kosen", "h-kosen"
            ]
        },
        "admin": {
            "gidNumber": 101,
            "memberUid": [
                "t-kosen"
            ]
        }
    }
    boxes = [
        {
            :name => "ubuntu-bionic",
            :box => "ubuntu/bionic64",
            :host_vars => {
                "ansible_python_interpreter" => "/usr/bin/python3",
                "ldap_server_passwd" => "hogefuga",
                "ldap_server_admin_passwd" => "hogefuga",
                "ldap_server_user_entries" => "#{ldap_server_user_entries.to_json}",
                "ldap_server_group_entries" => "'#{ldap_server_group_entries.to_json}'"
            }
        }
    ]
    host_vars = {}
    boxes.each do |opts|
        config.vm.define opts[:name] do |config|
            config.vm.box = opts[:box]
            host_vars[opts[:name]] = opts[:host_vars]
            if opts[:name] == boxes.last[:name]
                config.vm.provision "ansible" do |ansible|
                    ansible.playbook = "tests/test.yml"
                    ansible.limit = "all"
                    ansible.host_vars = host_vars
                end
            end
        end
    end
end
