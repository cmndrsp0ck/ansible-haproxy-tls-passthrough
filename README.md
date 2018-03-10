# ansible-haproxy-tls-passthrough
=========

This role will configure two haproxy nodes in an active-passive configuration on DigitalOcean Droplets. A simple redirect to https is enforced which is then passed to backends on port 443.

Role Variables
--------------

I recommend setting the *do_token* and *ha_auth_key* variables in **group_vars/*group_name*** and setting them to the values stored in an ansible-vault encrypted file in **group_vars/all/vault**

    # DigitalOcean access token
    do_token: "{{ vault_do_token }}"

    # Generated ha auth key.
    ha_auth_key: "{{ vault_ha_auth_key }}"

Just don't forget to set *vault_do_token* and *vault_ha_auth_key*.

You can adjust the following two variables in defaults/main.yml

    timezone: "America/Los_Angeles"
    locale: "en_US.UTF-8"


Example usage
----------------

Begin by installing the role.

    ansible-galaxy install -r requirements.yml

or

    ansible-galaxy install ansible-haproxy-tls-passthrough

Once the role is installed you can set it up in your playbook.

    - hosts: load_balancer
      roles:
          - { role: ansible-haproxy-tls-passthrough }
      become: True

License
-------

GPL-3.0
