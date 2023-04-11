[![CI](https://github.com/de-it-krachten/ansible-role-mattermost_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mattermost_docker/actions?query=workflow%3ACI)


# ansible-role-mattermost_docker

Sets up Mattermost using Docker.<br>
https://mattermost.com<br>



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8<sup>1</sup>
- RockyLinux 9<sup>1</sup>
- OracleLinux 8<sup>1</sup>
- OracleLinux 9<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- AlmaLinux 9<sup>1</sup>
- Debian 10 (Buster)<sup>1</sup>
- Debian 11 (Bullseye)<sup>1</sup>
- Ubuntu 18.04 LTS<sup>1</sup>
- Ubuntu 20.04 LTS<sup>1</sup>
- Ubuntu 22.04 LTS<sup>1</sup>
- Fedora 36<sup>1</sup>
- Fedora 37<sup>1</sup>
- Alpine 3<sup>1</sup>
- Docker dind (CI only)

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Wordpress FQDN
mattermost_fqdn: mm.example.com

# Retrieve SSL certificate from let's encrypt
mattermost_certbot: true

# Run nginx in docker
mattermost_nginx_docker: true

# Custom SSL certificate
# mattermost_ssl_key: /path/to/key
# mattermost_ssl_certificate_chain: /path/to/certificate/chain

# Max upload size
mattermost_max_upload_size: 100M
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'mattermost_docker'
  hosts: all
  become: "yes"
  vars:
    mysql_root_password: mattermost
    mysql_user: mattermost
    mysql_password: mattermost
    mysql_database: mattermost
    mattermost_certbot: False
    mattermost_domain: example.com
    mattermost_docker_data: /export/docker/mattermost
    mattermost_db_name: mattermost
    mattermost_db_user: mattermost
    mattermost_db_pwd: mattermost
    letsencrypt_email: "info@{{ mattermost_domain }}"
    letsencrypt_domain: "{{ mattermost_domain }}"
    letsencrypt_domains: "{{ [ mattermost_domain ] }}"
  roles:
    - deitkrachten.showinfo
    - deitkrachten.openssl
  tasks:
    - name: Include role 'mattermost_docker'
      ansible.builtin.include_role:
        name: mattermost_docker
</pre></code>
