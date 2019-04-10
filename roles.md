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
