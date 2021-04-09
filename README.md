# infra-word-e-moodle
Projeto que demostra a instalação e utilização inicial do **CMS WordPress** e do **AVA Moodle**.
+:warning: **Todos os procedimentos foram feitos em uma infraestrutura LAMP(Linux, Apache, MySQL e PHP) completamente funcional e em usuário root**
# Instalando o WordPress :pencil:
Comece Baixando o instalador tar.gz do WordPress
```bash
$ wget https://br.wordpress.org/latest-pt_BR.tar.gz
```
Aguarde o Download terminar de preferência que seja feito este comando na pasta root do Apache no meu caso **home/user/www** feito o download rode o comando:
```bash
$ tar -xvf latest-pt_BR.tar.gz
```
Dentro da pasta wordpress, renomeie o arquivo wp-config-sample.php para wp-config.php
```bash
$ mv wp-config-sample.php wp-config.php
```
Abra-o no editor de textos Nano
```bash
$ nano wp-config.php
```
E altere nome e senha do banco de dados, banco de dados este que deve ser criado no PhpMyAdmin com a base de dados nomeada como **wordpress**
Reinicie o Apache
```bash
$ /etc/init.d/apache2 restart
```
Feito isso acesse **localhost/wordpress** onde irá aparecer uma tela como a imagem abaixo, preencha os campos e clique Finalizar
(Print da tela)
Pronto! Você já possui seu primeiro site e ambiente Wordpress para trabalhar.
(Print da tela)
# Instalando o Moodle :pencil:
Para esse iremos precisar do navegador de terminal links
```bash
$ apt-get install links
```
Vamos começar baixando o nosso instalador tar.gz
```bash
$ links https://download.moodle.org/download.php/direct/stable310/moodle-3.10.3.tgz
```
Feito isso vamos descompactar em nossa pasta root do apache
```bash
$ tar -xvf moodle-3.10.3.tgz
```
Agora acesse o site **localhost/moodle** você verá a primeira tela do MOODLE, selecione a linguagem adequada para a instalação: Português – Brasil
Clique no botão **Next**
(Print da Tela)
O moodle irá fazer uma verificação no sistema e mostrará uma tela que serve para definir se o sistema é capaz de “rodar” o moodle ou não
Se todos os itens estiverem OK clique no botão Próximo
A próxima tela irá mostrar o endereço que será usado para acessar o moodle
Caso o endereço seja diferente é necessário alterá-lo no campo endereço web
O moodle também mostra nesta tela o diretório onde será instalado que no meu caso é o diretório **/home/user/www/moodle**
Crie o Diretório usando o comando 
```bash
$ mkdir /home/user/moodledata
```
É necessário também conceder ao diretório moodledata todos os privilégios de acesso usando o comando 
```bash
$ chmod 777 moodledata
```
Restart o apache 
```bash
$ /etc/init.d/apache2 restart
```
Atualize esta página da Web (F5)
E clique no botão **Próximo**
A próxima tela é muito importante pois se refere ao banco de dados do moodle, vamos aprender como criar a base de dados usando o programa **phpMyAdmin**
Abra outra janela do seu navegador padrão e digite **localhost/phpmyadmin**
Se pedir usuário e senha, coloque os dados do root
Na janela principal do phpMyAdmin digite no campo Criar novo banco de Dados a palavra **moodle** e clique no botão **Criar**
O Banco de dados então será criado...**

Volte a tela principal do phpMyAdmin e clique na opção **Privilégios**
Clique no botão **Adicionar novo usuário**

Na próxima tela devemos informar o nome do usuário, o Servidor onde será utilizado e também a Senha
**Nome do Usuário: moodle
Servidor: localhost
Senha: moodle**

No item **Privilégios globais** vamos clicar na opção **Marcar todos**
Para concluir a criação do usuário vamos clicar no botão **Executar**
Pronto! O usuário moodle foi criado com sucesso
Voltemos então para a instalação do moodle

Na tela de configuração do banco de dados devemos informar:
**Tipo do banco de dados: MySQL
Servidor hospedeiro do banco de dados: localhost
Base de dados: moodle
Usuário do banco: moodle
Senha do banco: moodle**
Para continuar a instalação clique no botão **Próximo**
O moodle fará outra verredura no sistema para verificar se o ambiente é compatível ou não

**Antes de continuar, vamos executar alguns passos:**
Entre no diretório cd **/home/user/www/moodle**
Digite o comando
```bash
$ cp config-dist.php config.php
``` 
Digite o comando
```bash
$ chmod 777 config.php
``` 
Edite o arquivo config.php
```bash
$ nano config.php
``` 
Que esta no diretório **/home/user/www/moodle**
Verifique as seguintes linhas:
**$CFG->dbtype = 'mysqli'; // mysql or postgres7 (for now)
$CFG->dbhost = 'localhost'; // eg localhost or db.isp.com
$CFG->dbname = 'moodle'; // database name, eg moodle
$CFG->dbuser = 'moodle'; // your database username
$CFG->dbpass = 'moodle'; // your database password
$CFG->prefix = 'mdl_'; // Prefix to use for all table names
Verifique a linha $CFG->wwwroot = 'http://localhost/moodle';
Verifique a linha $CFG->dirroot = '/home/user/www/moodle';
Verifique a linha $CFG->dataroot = '/home/user/moodledata';**
Elas devem estar exatamente deste jeito
Salve e feche o arquivo config.php

Volte a instalação do moodle e clique em **Continuar Instalação**
Na Próxima tela você poderá selecionar o pacote de idiomas mais adequado, em nosso caso vamos clicar em Baixar o pacote de idioma “Português – Brasil (pt_br)”
Para continuar a instalação clique no botão **Próximo**

Neste momento o moodle vai tentar confirmar a criação do arquivo c**onfig.php** em **/home/user/www/moodle**, por isso esse diretório deve ter privilégios de leitura e gravação
Caso ocorra algum erro durante esse processo, confirme novamente as configuações acima

A instalação deve continuar exibindo a tela sobre a licença do moodle
Para continuar clique no botão **Sim**
A próxima tela irá criar as tabelas no banco de dados do moodle
Todas as tabelas serão criadas agora
Ao final de cada tela de criação, deverá aparecer uma mensagem de Sucesso, continue até criar todas as tabelas com Sucesso
(Print da Tela)
Um backup será realizado e a mensagem de Sucesso deverá aparecer na tela
Continue clicando em **Continue**

Chegará na tela de configuração da conta admin que deverá ser utilizada pelo Administrador do sistema
Preencha de acordo com os dados solicitados, nome e senha coloque **admin**
Para concluir clique no botão **Atualizar Perfil**

Na próxima tela você deverá informar os dados da página principal do moodle
**Nome completo do seu site
Nome resumido do seu site
Descrição da página principal do moodle**
As próximas opções podem ser deixadas como padrão
Clique no botão **Save Changes**

**PRONTO! O MOODLE ESTÁ PRONTO PARA SER UTILIZADO.**
