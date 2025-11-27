#dnf module disable redis -y
#dnf module enable redis:7 -y
#
#dnf install redis -y
#
#sed -i -e '/protected-mode/ c protected-mode no' -e 's/127.0.0.1/0.0.0.0/' /etc/redis/redis.conf
#
#systemctl enable redis
#systemctl restart redis

- name: redis Setup
  hosts: all
  become: true
  tasks:
    - name: Install Ngnix 1.24
      ansible.builtin.dnf:
        name: 'redis:7'
        state: present

    - name: replace IP address
      ansible.builtin.replace:
        path: /etc/redis/redis.conf
        regexp: '127.0.0.1'
        replace: '0.0.0.0'

    - name: replace protected value no
      ansible.builtin.replace:
         path: /etc/redis/redis.conf
         regexp: 'protected-mode yes'
         replace: 'protected-mode no'

    - name: start redis services
      ansible.builtin.service:
         name: redis
         state: restarted
         enabled: yes