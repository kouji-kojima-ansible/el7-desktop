# EC2 CentOS7, RHEL7 に xrdp を インストールするロール (Role of setting EL7 Desktop)


Install role
------------

```
ansible-galaxy install kouji-kojima-ansible.el7-desktop --force
```

Process details
---------------

1. EPEL 有効化 (Enable EPEL)
2. Server with GUI インストール (Install Server with GUI group)
3. Xrdp インストール (Install Xrdp)
4. Xrdp 起動 (Run Xrdp)


Example site.yml
----------------

```
cat << EOF > site.yml
- hosts: servers
  remote_user: ec2-user
  become: yes
  vars:
    proxy_host: proxy.xxxxxxxxx.co.jp
    proxy_port: port_no
    no_proxys: xxxxx.co.jp,yyyy.co.jp
    ca_url: https://xxxxxxxx.co.jp/xxx.ca(*1)
    ca_sha256: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  roles:
    - { role: kouji-kojima-ansible.el7-desktop }
EOF
```


Example Hosts
-------------

```
# localhostの場合(In case of localhost)
cat << EOF > localhost
[servers]
localhost ansible_connection=local
EOF

# ステージング環境の場合(In case of staging environment)
cat << EOF > staging
[servers]
HostName or IP
HostName or IP

[all:vars]
ansible_ssh_user=ec2-user
EOF
```


Execute Playbook
-----------------

実行例(Normal execution)

```
# ローカルの場合(In case of localhost)
ansible-playbook -i localhost site.yml --private-key=/path/key.pem

# ステージング環境の場合(In case of staging environment)
ansible-playbook -i staging site.yml --private-key=/path/key.pem
```


License
-------

[Apache License Version 2.0](https://github.com/kouji-kojima-ansible/el7-desktop/blob/master/LICENSE)


Author Information
------------------

Kouji Kojima
