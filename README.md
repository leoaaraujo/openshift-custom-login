# Openshift Login - Customizing Login Page


* Run the playbook:

```
ansible-playbook playbook_custom_console.yaml -e "logotipo=/path/image.png" -e "bgcolor=colorname" -e "imagetype=png"
```


* Copy login-template.html for the all master servers in /etc/origin/master

```
rsync -avp login-template.html <user>@master-server:/etc/origin/master/
```


* Edit /etc/origin/master/master-config.yaml in all masters servers and add the lines below: 

```
oauthConfig:
  ....
  sessionConfig:
  ....
  templates:
    login: /etc/origin/master/login-template.html
```


* Restart all master api and controllers to apply

```
master-restart api api && master-restart controllers controllers
```
