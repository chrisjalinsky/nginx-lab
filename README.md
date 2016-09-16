# Nginx Plus Load Balancer lab environment

###Dependencies
* Ansible 2.0
* Vagrant 1.8.5
* Virtualbox 5.0.20 r106931


###Vagrantfile
The ```vagrant up``` command will, by default, build 3 hosts using the ansible/hosts.yaml API compatible file. Therefore we use the dynamic inventory script to read the hosts.yaml file. Adjust as necessary or use the static_inventory

###Prerequisites
* You need to get a trial key and certificate to authenticate with the NginX Plus Apt repo.

####Place the Nginx Repo key and cert in the ansible nginx role files folder
Name them ```nginx-repo.key``` and ```nginx-repo.crt``` and place them in the
```
./ansible/roles/nginx/files/etc/ssl/ngninx/ directory
```

###Ansible Playbooks

Run the playbooks from the project's ansible/ directory. Looking at the playbooks, you can see variables passed into the role, that alters the functionality. There are 2 configurations. A load balancer for proxying SSL TCP requests (provision_nginx_lb.yaml). And SSL/HTTP server configurations with or without self signed certificates (provision_nginx_upstream.yaml).
```
ansible-playbook provision_nginx_lb.yaml -i inventory.py
ansible-playbook provision_nginx_upstream.yaml -i inventory.py
```
###Nginx

####Nginx Plus Upstream Dashboard
```
http://10.10.0.102:8888/status.html#tcp_upstreams
```

####Test the round robin load balancing
```
curl -k https://10.10.0.102:443
```
