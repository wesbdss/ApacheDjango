 # Configuração Servidor Python (Django) + Apache + Ubuntu Server para idiotas
 
 ### Requisitos
> Versão S.O. usada: Ubuntu Server 18.05 LTS
> Versão python usado: 3>

O uso do apache é opcional pode ser usado outros distribuidores como nginx.
- Apache2
```sh
$ sudo pip install apache2
```
- Python 3
```sh
$ sudo apt-get install python3-pip
```
- VirtualEnv
```sh
$ pip3 -m install virtualenv
```
Após isso, crie um ambiente virtual usando virtualenv.
```sh
$ python3 virtualenv "Nome do Projeto"
```
O ambiente virtual serve para que seus projetos em python não entrem em conflito.
> O nome do projeto não vai influenciar no site, serve apenas para não gerar conflito na sua máquina.

Entre no ambiente virtual:
```sh
$ source "Nome do Projeto"/bin/activate
```
se aparecer:
```sh
("nome do projeto") user@nomeserver~
```
então funcionou :)

instale o Django:
```sh
("nome do projeto") user@nomeserver~ pip install django
```
crie o projeto em django:
```sh
("nome do projeto") user@nomeserver~  django-admin startproject "nome do site"
```

teste ele:
```sh
("nome do projeto") user@nomeserver~ python "nome do site"/manage.py runserver
```
se rodou rodou, se não rodou vc rodou. 
Dê ctrl+C
Saia do seu ambiente virtual:
```sh
("nome do projeto") user@nomeserver~deactivate
```
### Configurando o Apache para receber o Django
```sh
user@nomeserver~nano /etc/apache2/sites-avaliable/000-default.conf
```
Vá para o final do arquivo
```sh
    ...
    </VitualHost>
# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```
Cole essa configuração antes do </VitualHost>

```
        ...
        Alias /static /home/user/"Nome do site"/static
        <Directory /home/user/"Nome do site"/static>
            Require all granted
        </Directory>
        <Directory /home/user/"Nome do site"/"Nome do site">
            <Files wsgi.py>
                Require all granted
            </Files>
        </Directory>
        WSGIDaemonProcess "Nome do projeto" python-home=/home/user/"Nome do projeto" python-path=/home/user/"Nome do site"
        WSGIProcessGroup "Nome do site"
        WSGIScriptAlias / /home/user/"nome do site"/"nome do site"/wsgi.py
    </VitualHost>
```
execute: 
```sh
user@nomeserver~ sudo service apache2 restart
```
```sh
user@nomeserver~ sudo service apache2 status
```
>Se der tudo certo, então seu projeto ja pode começar a ser desenvolvido.

### Feito por Wesbdss
