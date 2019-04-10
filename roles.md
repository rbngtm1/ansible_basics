1. create a folder called roles inside ansible directory
2. let's try ansible-galaxy init httpd --offline 
3. command: tree and see the branches 
4. Inside httpd folder, you have many directories
5. Inside tasks directory, you will see something called main.yml (which will match dependencies for your variable)
6. let's edit the main.yml file with something like below:
```yml
---
- name: Installing httpd
  yum:
    name: httpd
    state: latest
  notify: restart httpd
- name: copying the file
  copy:
    src: index.html
    dest: "{{ dest }}/index.html"
    mode: 0766
  notify: restart httpd
```
7. Let's have our source file (index.html) inside files directory
8. vi index.html and write sth
9. Let's go to handlers directory and change main.yml file with something below:
```yml
---
- name: restart httpd
  service:
    name: httpd
    state: restarted
```
10. Let's go inside var directory and edit the main.yml
```yml
dest: "var/www/html"
```
##### Note: Your default path for ansible roles is set inside /etc/ansible/ansible.cfg --vi and search for sth with ansible_path, you may change the path as per your need

1. Let's go insible playbook directory and create file with something like rolegiven.yml
```yml
---
- name: Installing httpd
  hosts: mr.india
  become: true
  roles:
    - ../roles/httpd
```
