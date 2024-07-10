Relatório Explicativo do Desafio de Pipeline de Dados

Introdução
O objetivo deste desafio é construir um pipeline de dados que extrai informações de duas fontes distintas: um banco de dados PostgreSQL e um arquivo CSV. Essas informações devem ser armazenadas localmente e, posteriormente, carregadas em um banco de dados PostgreSQL final. A tarefa envolve o uso de ferramentas específicas: Airflow para orquestração, Meltano para carregamento de dados e PostgreSQL como banco de dados.

Ferramentas Utilizadas
Airflow: Ferramenta de orquestração para automatizar, monitorar e gerenciar os fluxos de trabalho.
Meltano: Ferramenta de extração, transformação e carregamento (ETL) escrita em Python.
PostgreSQL: Sistema de gerenciamento de banco de dados relacional.

Passo a Passo da Solução
1. Configuração do Ambiente
a. Criação do Ambiente Virtual
Para garantir que todas as dependências do projeto sejam instaladas corretamente, criamos um ambiente virtual na pasta do projeto e ativamos o ambiente virtual. Verificamos se estamos com a última versão do pip para evitar problemas de compatibilidade.

b. Instalação das Bibliotecas Necessárias
Instalamos as bibliotecas necessárias para o projeto, como pandas para manipulação de dados. Criamos um arquivo requirements.txt para salvar as versões das bibliotecas utilizadas e garantir a replicabilidade do ambiente.

2. Configuração do Banco de Dados
a. Configuração do Docker para o PostgreSQL
Usamos o Docker para configurar e iniciar uma instância do PostgreSQL. Criamos um arquivo docker-compose.yml especificando a imagem do PostgreSQL e configuramos as variáveis de ambiente necessárias (usuário, senha e nome do banco de dados). Iniciamos o banco de dados utilizando o comando docker-compose up.

3. Configuração do Airflow
a. Instalação do Airflow
Instalamos o Airflow utilizando o Docker. Criamos um arquivo docker-compose.yml especificando a imagem do Airflow e configuramos as variáveis de ambiente necessárias. Definimos os volumes para armazenar os DAGs, logs e plugins. Iniciamos o Airflow com o comando docker-compose up -d e acessamos a interface do Airflow através do navegador no endereço http://localhost:8080.

b. Criação dos DAGs no Airflow
Criamos os DAGs no Airflow para orquestrar as tarefas de extração e carregamento dos dados. Cada DAG é composto por tarefas que executam funções específicas para extrair dados do PostgreSQL e do CSV, armazenar esses dados localmente e, posteriormente, carregá-los no banco de dados final.

4. Extração dos Dados
a. Extração dos Dados do PostgreSQL
Utilizamos a biblioteca psycopg2 para conectar ao banco de dados PostgreSQL e extrair os dados das tabelas. Executamos uma consulta SQL para selecionar todos os registros da tabela orders e armazenamos esses dados em um arquivo CSV, seguindo a estrutura de diretórios especificada (/data/postgres/orders/{data}/).

b. Extração dos Dados do CSV
Carregamos os dados do arquivo CSV utilizando a biblioteca pandas e armazenamos esses dados em um arquivo CSV local, seguindo a estrutura de diretórios especificada (/data/csv/{data}/).

5. Carregamento dos Dados no PostgreSQL
Conectamos ao banco de dados PostgreSQL utilizando psycopg2 e carregamos os dados extraídos (tanto do PostgreSQL original quanto do CSV) no banco de dados final. Utilizamos a função to_sql da biblioteca pandas para inserir os dados nas tabelas correspondentes (orders e order_details).

Considerações Finais
Este relatório detalha a implementação de um pipeline de dados que extrai informações de um banco de dados PostgreSQL e de um arquivo CSV, armazena esses dados localmente e, finalmente, carrega-os em um banco de dados PostgreSQL final. Utilizamos o Airflow para orquestrar as tarefas e o Meltano para a manipulação dos dados.

Instruções para Execução

Clone o repositório do projeto.
Crie e ative o ambiente virtual.
Instale as dependências listadas em requirements.txt.
Configure e inicie o Docker.
Inicie o Airflow e verifique os DAGs.
Execute o pipeline pelo Airflow.

A estrutura modular e idempotente do pipeline garante que ele possa ser executado diariamente, com as etapas de escrita e leitura separadas, permitindo a reexecução de etapas específicas conforme necessário.

