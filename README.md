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

* Before the restart, access your console:

<img width="595" alt="01" src="https://github.com/leoaaraujo/openshift-custom-login/blob/2f6a781599dc64f38efc5056b74ceb06b2f38a9d/custom-login.png">
