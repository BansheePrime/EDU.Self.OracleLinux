## Full credit to @glmrenard; here's a version I adapted for Percona server 5.7 on Ubuntu 16.04:
<https://stackoverflow.com/questions/38433295/unable-to-change-password-for-root-account-ansible>

---
#Reset MySQL root password
- name: Stop MySQL
  systemd:
    name: mysql
    state: stopped

- name: set environment variables
  shell: systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"

- name: Start MySQL
  systemd:
    name: mysql
    state: started

- name: Reset root PW
  command: mysql -u root --execute="UPDATE mysql.user SET authentication_string = PASSWORD('{{ mysql_rootpw }}') WHERE User = 'root' AND (Host = 'localhost' OR Host = '127.0.0.1');"

- name: Flush MySQL privileges
  command: mysql -u root --execute="FLUSH PRIVILEGES"

- name: Stop MySQL
  systemd:
    name: mysql
    state: stopped

- name: Unset environment variables
  shell: systemctl unset-environment MYSQLD_OPTS

- name: Start MySQL
  systemd:
    name: mysql
    state: started

## 
<https://dba.stackexchange.com/questions/274547/cant-set-root-password-after-fresh-installation-of-mariadb-using-ansible>

- name: update mysql root password for root account
  mysql_user:
    name: root
    login_unix_socket: /var/run/mysqld/mysqld.sock
    host: 'localhost'
    password: '{{ mysql_root_password }}'
    priv: "*.*:ALL,GRANT"
    check_implicit_admin: true


### p. 31 create user
<https://phoenixnap.com/kb/how-to-create-new-mysql-user-account-grant-privileges>
sudo mysql –u root –p
SELECT user,host FROM mysql.user;
CREATE USER 'django'@'%' IDENTIFIED BY '1234';
GRANT INSERT ON *.* TO 'django'@'%';
SELECT user,host,password,show_db_priv FROM mysql.user;

### 
app1 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222 ansible_ssh_user='vagrant' ansible_ssh_private_key_file='/home/gidra/.vagrant.d/insecure_private_key'
app2 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2200 ansible_ssh_user='vagrant' ansible_ssh_private_key_file='/home/gidra/.vagrant.d/insecure_private_key'
db ansible_ssh_host=127.0.0.1 ansible_ssh_port=2201 ansible_ssh_user='vagrant' ansible_ssh_private_key_file='/home/gidra/.vagrant.d/insecure_private_key'