filebeat
=========

This role installs and configures filebeat for log collection output towards an ELK stack (Logstash instance)

Requirements
------------

None


Role Variables
--------------

Default variables (with default values in defaults/main.yml) :
* docker_userns_remap : whether remapping of user namespace is being used for Docker (security feature defaults to true)
* dockremap_subuid : first subuid used for user namespace remap for Docker (defaults to 165536) - should be retrieved by docker_server role in host_vars
* dockremap_subgid : first subgid used for user namespace remap for Docker (defaults to 165536) - should be retrieved by docker_server role in host_vars
* logstash_host : host or IP where logstash instance is located (defaults to localhost)
* logstash_port : TCP port on which logstash instance is listening (defaults to 5044)
* logstash_tls_crt : TLS cert used for securely connect to logstash instance (defaults to dummy cert)
* log_collection : whether to collect logs or not (defaults to true), could be set distinctly for each host


Variables from vars directory:
* OS specific (RedHat.yml / Debian.yml) :
  * packages_to_install : list of packages to install on server
* Global (main.yml):
  * elastic_gpg_key_url: URL for retrieving Elastic GPG key
  * elastic_packages_url: URL for retrieving Elastic APT/YUM packages


Dependencies
------------

This roles depends upon completion of docker_server role (for collecting correct dockremap subuid/gid).

Example Playbook
----------------

    - hosts: full_maintenance
      gather_facts: true
      become: true
      roles:
      - { role: filebeat, tags: filebeat }
      vars:
      - { docker_userns_remap: true }
      - { logstash_host: "localhost" }
      - { logstash_port: 5044 }
      - { log_collection: true }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
