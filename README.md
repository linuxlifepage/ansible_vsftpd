## ANSIBLE PLAYBOOK VSFTPD WITH TLS

- Copy ssh-key to host

```
ssh-copy-id -i ssh/id_rsa.pub ubuntu@77.77.77.77
```

- Set password for ftp

```
vim roles/defaults/main.yml

...
user_name: ftpuser
user_password: YOUR_PASSWORD
```

- Set cert data

```
vim roles/defaults/main.yml

...
openssl_csr_cn: mysite.com
openssl_csr_subject: CN=mysite.com,ST=MOW,L=Moscow
openssl_csr_subject_alt: "DNS:mysite.com,DNS:www.mysite.com"
organization_name: "MySite"
```

- Run playbook

```
ansible-playbook vsftpd.yaml
```

- Open ports

```
UFW:
sudo ufw allow 20-21/tcp
sudo ufw allow 12000-12005/tcp

IPTABLES:
iptables -A INPUT -p tcp --dport 20:21
iptables -A INPUT -p tcp --dport 12000:12005  
```

- Test with filezilla/Cyberduck


