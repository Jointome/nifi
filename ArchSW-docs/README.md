#Arquitetura de Software
##nifi da apache
###Descrição
Nifi é uma interface gráfica criada para automatizar fluxos de dados entre diversas redes de computadores mesmo quando os protocolos diferem.

###Instalação
Para podermos instalar o projecto é necessário instalar o maven. Logo usa-se o comando `sudo apt-get install maven` o que pode resultar na instalaçâo de uma versão antiga(verificar com o comando `mvn -version`). Caso a versão seja inferior 3.1.0 deve ir a 

`https://maven.apache.org/download.cgi` 

fazer download e seguir os passos na seguinte ligação 

`https://maven.apache.org/install.html`.

De seguida devemos através da linha de comandos aceder ao diretorio do projeto e correr o comando 

`mvn clean install`

 e esperar que acabe o que pode demorar.
No final deve aceder ao diretório 

`nifi-assembly` 

que se encontra no projeto. Correr o comando 

`ls -lhd target/nifi*`

 para verificar qual a versão do nifi tem presente e de seguida os comandos 
 
`mkdir ~/example-nifi-deploy`

`tar xzf target/nifi-*-bin.tar.gz -C ~/example-nifi-deploy`

`ls .l ~/example-nifi-deploy/`

###Execução
Para executar na linha de comandos inserir o comando 

`cd ~/example-nifi-deploy/nifi-*`

`./bin/nifi.sh start`

No explorador de internet:

http://localhost:8080/nifi/
