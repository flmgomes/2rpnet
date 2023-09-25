# 2rpnet

1ª Tarefa: Criar uma conta gratuita na GCP, Azure ou AWS, usando apenas as camadas 
gratuitas e/ou créditos.

- Google Cloud Platform (GCP):
Acesse o site do Google Cloud Platform.
Clique em "Comece gratuitamente".
Você será solicitado a entrar em sua conta do Google ou criar uma se você ainda não tiver.
Siga as etapas de configuração, que incluirão a inserção das informações de pagamento. Nota: Mesmo para a camada gratuita, o Google pede detalhes do cartão de crédito para evitar abusos. No entanto, eles não o cobrarão sem sua autorização explícita.
Depois de configurar, você receberá um crédito promocional para explorar os serviços pagos.

- Microsoft Azure:
Acesse o site da Microsoft Azure.
Clique em "Comece gratuitamente".
Faça login com sua conta Microsoft ou crie uma.
Forneça os detalhes de pagamento, novamente, como uma medida para evitar abusos.
Uma vez configurado, você receberá um crédito promocional para ser usado no primeiro mês, além de acesso a uma variedade de serviços gratuitos por 12 meses.
Amazon Web Services (AWS):

- Visite o site da AWS Free Tier.
Clique em "Crie uma conta gratuita".
Insira seus detalhes para criar uma conta da AWS.
Forneça informações de pagamento.
Confirme sua identidade por meio de uma ligação telefônica ou SMS.
Selecione o plano de suporte desejado (para fins gratuitos, selecione o plano "Basic").
Depois de configurar, você terá acesso ao nível gratuito da AWS, que oferece uma quantidade específica de recursos e serviços gratuitos durante 12 meses e algumas ofertas que são sempre gratuitas.

_________________________________________

2ª Tarefa: Criar uma máquina virtual com uma imagem Linux.

- Google Cloud Platform (GCP):
Faça login no Google Cloud Console.
Selecione o projeto desejado ou crie um novo projeto.
No menu à esquerda, vá para "Compute Engine" > "VM instances".
Clique em "Create".
Nomeie sua VM, selecione a região e zona.
No campo "Boot Disk", selecione a imagem Linux desejada (por exemplo, Debian, CentOS, Ubuntu).
Configure o tamanho do disco e o tipo, se necessário.
Selecione o tipo de máquina (e.g., "f1-micro" para instâncias pequenas).
Configure quaisquer outras opções conforme necessário, como redes, etiquetas, etc.
Clique em "Create".

- Microsoft Azure:
Faça login no Portal do Azure.
No menu à esquerda, clique em "Create a resource".
Na barra de pesquisa, digite "Linux" e selecione a distribuição desejada (por exemplo, Ubuntu Server).
Clique em "Create".
Preencha os detalhes da instância, como nome, tamanho da VM, região, etc.
Configure detalhes adicionais, como discos, redes e outros, conforme necessário.
Clique em "Review + create" e, após verificar as configurações, clique em "Create".

- Amazon Web Services (AWS):
Faça login no AWS Management Console.
No menu "Services", vá para "EC2".
Clique em "Launch Instance".
Na etapa "Choose an Amazon Machine Image (AMI)", selecione uma imagem Linux desejada (por exemplo, "Amazon Linux 2 AMI" ou "Ubuntu Server").
Escolha um tipo de instância (por exemplo, "t2.micro" para instâncias gratuitas no tier gratuito).
Configure os detalhes da instância, como armazenamento, tags, redes e grupos de segurança.
Revise e clique em "Launch".
Se solicitado, selecione um par de chaves (key pair) existente ou crie um novo. Esse par de chaves permitirá que você se conecte à sua VM por SSH.
Após criar a VM em qualquer uma dessas plataformas, você pode se conectar a ela usando SSH (se permitido pelas configurações de segurança). Assegure-se de ter o endereço IP adequado (público ou privado, dependendo da sua configuração) e, se necessário, a chave privada correspondente ao par de chaves selecionado (especialmente no caso da AWS).

_________________________________________

3ª Tarefa: Realizar o setup da ferramenta Grafana, utilizando Docker, e acessar via 
navegador a interface Web, provando seu correto funcionamento.

- Instalação do Docker:

Para sistemas baseados em Debian/Ubuntu:

sudo apt update
sudo apt install docker.io

Para sistemas baseados em CentOS/RHEL:

sudo yum install docker

2. Iniciar o Docker:

Para sistemas baseados em Debian/Ubuntu/CentOS:

sudo systemctl start docker
sudo systemctl enable docker

- Executar o Grafana usando Docker:

sudo docker run -d -p 3000:3000 grafana/grafana

Este comando faz o seguinte:
-d significa que o Docker executará o contêiner em segundo plano.
-p 3000:3000 mapeia a porta 3000 do contêiner para a porta 3000 do seu host.
grafana/grafana é a imagem oficial do Grafana no Docker Hub.

4. Acessar o Grafana via navegador:

http://seu_ip:3000
Por padrão o usuário e a senha são ambos admin.

5. Configurar senha:
Na primeira vez que você fizer login, o Grafana solicitará que você altere a senha.

7. Prova de funcionamento:
Depois de fazer login, você será levado ao painel inicial do Grafana. Você pode criar um novo "Dashboard" ou adicionar uma fonte de dados para começar a criar gráficos. Para uma prova rápida de funcionamento, basta você estar na interface web, capaz de fazer login e navegar pelos menus.

_________________________________________

4ª Tarefa: Realizar o setup de banco de dados relacional, utilizando Docker. Acessar o CLI 
do banco e provar seu funcionamento correto com alguns comandos de listagem ou similar. 
(Bancos sugeridos: PostgreSQL; MySQL; SQLite; ou similar)

1. Configurar o PostgreSQL com Docker:
a. Executar a imagem do PostgreSQL:

sudo docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres

Isso fará o seguinte:
--name some-postgres: Atribui o nome "some-postgres" ao contêiner.
-e POSTGRES_PASSWORD=mysecretpassword: Define uma senha para o superusuário "postgres".
-d postgres: Especifica que queremos executar o contêiner em segundo plano usando a imagem "postgres".
b. (Opcional) Se você quiser mapear a porta e o volume para tornar os dados persistentes:

sudo docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -v /path/to/local/folder:/var/lib/postgresql/data -d postgres
-p 5432:5432: Mapeia a porta 5432 do contêiner para a porta 5432 do host.
-v /path/to/local/folder:/var/lib/postgresql/data: Monta o volume para persistir os dados do banco de dados. Substitua /path/to/local/folder pelo caminho onde você deseja armazenar os dados do PostgreSQL no seu host.

2. Acessar o CLI do PostgreSQL:
- Execute o seguinte comando para acessar o bash do contêiner:

sudo docker exec -it some-postgres bash
b. Depois de entrar no bash do contêiner, acesse o CLI do PostgreSQL com:
psql -U postgres

3. Provar seu funcionamento:
Agora que você está no CLI do PostgreSQL, você pode executar comandos SQL.

a. Listar todos os bancos de dados:
\l

b. Criar um novo banco de dados:
CREATE DATABASE testdb;

c. Listar novamente para ver o novo banco de dados:
\l

d. Conectar-se ao novo banco de dados:
\c testdb

e. Criar uma nova tabela, inserir alguns dados e consultar:
CREATE TABLE test_table (id serial primary key, name varchar(50));
INSERT INTO test_table (name) VALUES ('John'), ('Doe');
SELECT * FROM test_table;

Se você vir os dados que inseriu na tabela test_table, seu PostgreSQL está funcionando corretamente!

Para sair do CLI do PostgreSQL, digite:
\q

_________________________________________

5ª Tarefa: Realizar o setup de um Servidor Web, utilizando Docker. Deve ser publicado uma 
página simples de HTML, e ser acessada via browser para provar seu correto funcionamento.
(Servidores sugeridos: Xampp, JBoss, ou similar)

1. Criar uma página HTML simples:
mkdir mywebsite
echo "<h1>Bem-vindo ao meu website via Docker!</h1>" > mywebsite/index.html

2. Configurar o servidor Nginx usando Docker:
a. Execute a imagem do Nginx, mapeando a porta e montando o volume para nossa página HTML:
sudo docker run --name mynginx -p 80:80 -v /path/to/mywebsite:/usr/share/nginx/html:ro -d nginx
Substitua /path/to/mywebsite pelo caminho absoluto do diretório mywebsite que você criou anteriormente. O que este comando faz é:

--name mynginx: Dá o nome "mynginx" ao contêiner.
-p 80:80: Mapeia a porta 80 do contêiner para a porta 80 do host, que é a porta padrão para HTTP.
-v /path/to/mywebsite:/usr/share/nginx/html:ro: Monta o diretório mywebsite do host no diretório padrão de conteúdo web do Nginx no contêiner. O ro garante que o montagem seja somente leitura.
-d nginx: Indica que queremos executar o contêiner em segundo plano usando a imagem "nginx".

3. Acessar o servidor via browser:
Abra seu navegador web e navegue até:
http://localhost
Você deve ver a mensagem "Bem-vindo ao meu website via Docker!".

_________________________________________

6ª Tarefa: Criar um dashboard no Grafana de monitoramento do CPU, RAM, Disco e Rede, 
da própria máquina virtual. Adicionar o monitoramento do banco de dados e do servidor web 
instalados previamente. Adicionalmente, podem ser gerados gráficos de monitoramentos que 
julgar mais relevantes. 

1. Configuração do Prometheus e node_exporter:
1.1. Inicie o Prometheus e o node_exporter usando Docker:
# Node Exporter
sudo docker run -d --net="host" --pid="host" -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter --path.rootfs=/host
# Prometheus
sudo docker run -d -p 9090:9090 -v /path/to/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
No exemplo acima, substitua /path/to/prometheus.yml pelo local onde você armazenou o arquivo de configuração do Prometheus.

1.2. O conteúdo mínimo do prometheus.yml seria:
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node'
    static_configs:
      - targets: ['localhost:9100']

2. Configurar Exportadores para PostgreSQL e Nginx:
2.1. Para PostgreSQL, você pode usar o pg_exporter.
2.2. Para Nginx, você pode usar o nginx-vts-exporter se estiver usando o módulo VTS com o Nginx. Ou o nginx-prometheus-exporter se não estiver usando o VTS.

3. Configuração no Grafana:
3.1. Adicione o Prometheus como fonte de dados:
Acesse Grafana -> Configurações (engrenagem no canto inferior esquerdo) -> Fontes de Dados -> Adicionar fonte de dados.
Escolha Prometheus.
Configure o URL. Se o Prometheus estiver rodando na mesma máquina que o Grafana, use http://localhost:9090.
3.2. Crie um novo Dashboard e comece a adicionar painéis:
Para CPU, RAM, Disco e Rede: Use as métricas fornecidas pelo node_exporter como node_cpu_seconds_total, node_memory_MemAvailable_bytes, node_filesystem_avail_bytes, node_network_transmit_bytes_total, etc.
Para PostgreSQL: Dependendo do exportador, você terá métricas específicas disponíveis. Geralmente, eles começam com pg_.
Para Nginx: Dependendo do exportador, você terá métricas específicas disponíveis, como nginx_requests_total, nginx_upstream_peers_responses_5xx_total, etc.

4. Painéis Adicionais:
Além das métricas básicas, você pode querer monitorar:
Carga média do sistema.
Uso de espaço em disco por diretório ou serviço.
Número de conexões ativas no seu banco de dados ou servidor web.
Latência da rede ou latência nas respostas do servidor web.
Taxa de erros em seus serviços.

_________________________________________

7ª Tarefa: Criar regras de alertas de ao menos três componentes monitorados. Os alertas 
devem enviar e-mails, para sua conta pessoal como destinatário, a fim de validar o 
funcionamento correto do alerta. 

8ª Tarefa: Aplicar políticas de acesso ao Grafana, onde os usuários sysadmin@2rpnet.com 
e academy@2rpnet.com devem possuir acesso de administração e o people@2rpnet.com 

9ª Tarefa: Apresentar/Documentar o custo previsto dos componentes utilizados caso fosse 
uma solução produtiva, e mostrar detalhadamente abordagens para otimizar esse custo, 
como por exemplo exploração de quotas.



