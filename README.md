## :books: ElasticHQ - Management and Monitoring for Elasticsearch.

Ao configurar um cluster de Elastic, é possível também configurar o painel ElasticHQ para fins de monitoramento. Basta seguir os passos abaixo:

### **Requisitos**

-   Elasticsearch à partir da versão 5.x
-	Python 3.4+

### **Instalação**
----------

Baixe e descompacte o conteúdo do arquivo zip no path /var/lib/elastichq

```sh
$ sudo git clone https://github.com/ElasticHQ/elasticsearch-HQ /var/lib/elastichq
```

Instale o pip3 (caso não esteja instalado)

```sh
$ sudo apt install python3-pip
```

Navegue para o path /var/lib/elastichq  e instale usando o pip3

```sh
$ sudo -H pip3 install -r requirements.txt
```

Inicie a aplicação:
```sh
$ sudo python3 application.py
```

Acesse via navegador:
```sh
$ http://seuip:5000
```

### **Testando o acesso**
----------

É possível testar o funcionamento dessa ferramenta, subindo um ELK, depois basta acessar informar o endereço do cluster dentro do ElasticHQ
 
No link à seguir tem um projeto com mais detalhes: https://github.com/leandro-matos/docker-elastic-kibana 

Também é possível efetuar os testes usando o docker-compose.yml desse projeto.


#### **Criando o daemon do elastichq**
----------

Criando o arquivo de configuração:
```sh
$ sudo vi /lib/systemd/system/elastichq.service
```

Basta adicionar o script abaixo para criação do serviço
```sh
[Unit]

Description=Elastic HQ

After=multi-user.target

Conflicts=getty@tty1.service

[Service]

Type=simple

ExecStart=/usr/bin/python3 /var/lib/elastichq/application.py

StandardInput=tty-force

User=root

StandardOutput=journal

[Install]

WantedBy=multi-user.target
```

Reload do daemon
```sh
$ sudo systemctl daemon-reload
```
Habilitar o serviço
```sh
$ sudo systemctl enable elastichq.service
```
Iniciar o serviço
```sh
$ sudo systemctl start elastichq.service
```
Checar o status
```sh
$ sudo systemctl status elastichq.service
```

### **Alguns exemplos de visualização por meio do ElasticHQ**
----------

![](images/elastichq-index.PNG)

![](images/elastichq-index2.PNG)


## **Links Úteis**
* [Documentação Oficial](http://docs.elastichq.org/installation.html)
* [Site oficial](https://www.elastichq.org/)
----------

Leandro de Matos Pereira |
leandromatpereira@hotmail.com