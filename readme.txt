# File: /etc/ansible/roles/use-proxy/readme.txt

# Overview
This ansible role, use-proxy, is designed to make it easier for ansible to set up a reverse ssh tunnel to a host that is running a web proxy, for tasks to use that proxy.

# How to configure
Check out vars/main.yml and update these values:

proxy_port: 3128
local_proxy_port: "{{proxy_port}}"
proxy_server: tunnel@server@example.net
proxy_server_ssh_port: 22

# Dependencies
* An available ssh host that also provides a web proxy, such as apache with a proxy config or squid.
* Automatic ssh authentication to that server. You can use anything that provides this, but ssh keys is the easiest.

# How to use in a playbook
Just comment the - use-proxy item in the roles list to exclude the proxy.
---
- name: Playbook that uses an ssh tunnel for http_proxy
  hosts: test
  remote_user: root
  environment: "{{ proxy_env | default(omit) }}"
  roles:
    - use-proxy
    - example
