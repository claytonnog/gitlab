# Gitlab

### Instalando

Primeiro subimos o container lxc:
```
$ lxc launch ubuntu:18.04 gitlab-teste
```

Entramos no container:
```
$ lxc exec gitlab-teste bash
```

Instalamos os pacotes necessários:
```
# apt update && apt install -y curl openssh-server ca-certificates
# apt install -y postfix # para posterior envio de e-mail
# curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | bash
# ip a
# EXTERNAL_URL="https://10.197.234.72" apt install gitlab-ee
```

Usamos o "ip a" para saber qual o ip do container que vamos utilizar na instalação e inicialização do gitlab

Após a instalação faça o acesso via browser e configure a senha de acesso, o usuário é root.

OBS: provavelmente ele reclame algo sobre o acesso via https, sobre não ter certificado válido. Não tem problema agora.

### Na maquina cliente

Na maquina cliente, vamos agora inicializar nosso repositório:

```
$ mkdir ruby-api-rest/
$ cd ruby-api-rest/
$ git config --global user.name "Clayton Neves"
$ git config --global user.email "clayton.nog@gmail.com"
$ git init
$ git config --global user.name "Clayton Neves" 
$ git add
$ git commit -m "first commit"
$ git push --set-upstream origin master
```

No push, ele vai dar um erro, algo do tipo:
```
fatal: unable to access 'http://10.197.234.72/devops-engineer/ruby-api-rest.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
```

Como nosso servidor do gitlab não tem certificado válido, o git está reclamando.

Precisamos rodar o comando abaixo para que o git permita o push no servidor sem certificado válido:
```
$ git config --global http.sslverify false
```

Após isso, com certeza vai funcionar.
```
$ git push --set-upstream origin master
```


#### OBS: não esqueça de criar o grupo e o projeto no gitlab
