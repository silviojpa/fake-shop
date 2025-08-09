# Fake Shop


## Variável de Ambiente
DB_HOST	=> Host do banco de dados PostgreSQL.

DB_USER => Nome do usuário do banco de dados PostgreSQL.

DB_PASSWORD	=> Senha do usuário do banco de dados PostgreSQL.

DB_NAME	=>	Nome do banco de dados PostgreSQL.

DB_PORT	=>	Porta de conexão com o banco de dados PostgreSQL.

-----------------------------------------------------------------------------

Fake Shop
Este é um projeto de uma loja virtual de exemplo, chamada "Fake Shop", desenvolvida com Flask e PostgreSQL. A aplicação é totalmente containerizada com Docker para facilitar a execução em ambientes de desenvolvimento e produção.

🏛️ Arquitetura
Backend: Python com o micro-framework Flask.

Banco de Dados: PostgreSQL.

Containerização: Docker e Docker Compose.

Migrações de Banco: Alembic com Flask-Migrate.

Servidor WSGI: Gunicorn.

🚀 Como Executar o Projeto Localmente
Para executar este projeto, você precisará ter o Docker e o Docker Compose instalados em sua máquina.

Pré-requisitos
Docker

Docker Compose (geralmente já vem incluído no Docker Desktop)

Passo a Passo
Clone o Repositório

git clone <URL_DO_SEU_REPOSITORIO>
cd <NOME_DA_PASTA_DO_PROJETO>

Crie o arquivo docker-compose.yml
Certifique-se de que o arquivo docker-compose.yml que criamos está na raiz do seu projeto.

Construa e Inicie os Containers
No terminal, na raiz do projeto, execute o seguinte comando:

docker-compose up --build

O comando up inicia os containers definidos no docker-compose.yml.

A flag --build força a reconstrução da imagem da sua aplicação, garantindo que quaisquer alterações no código sejam aplicadas.

O terminal exibirá os logs do banco de dados e da aplicação Flask. O script entrypoint.sh irá automaticamente aplicar as migrações do banco (flask db upgrade) antes de iniciar o servidor.

Acesse a Aplicação
Após os containers estarem em execução, abra seu navegador e acesse:
http://localhost:5000

Parando a Aplicação
Para parar todos os containers, pressione Ctrl + C no terminal onde o docker-compose está rodando. Para remover os containers e a rede criada, execute:

docker-compose down

Se quiser apagar também o volume do banco de dados (todos os dados serão perdidos), use:

docker-compose down -v

⚙️ Variáveis de Ambiente
As variáveis de ambiente são gerenciadas diretamente no arquivo docker-compose.yml para o ambiente de desenvolvimento.

Variável

Descrição

Valor Padrão

DB_HOST

Host do banco de dados PostgreSQL.

postgre

DB_USER

Nome de usuário do banco.

fakeshop

DB_PASSWORD

Senha do banco de dados.

Pg1234

DB_NAME

Nome do banco de dados.

fakeshop

FLASK_APP

Arquivo principal da aplicação Flask.

index.py
