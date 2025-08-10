💡 Dica Rápida: Rodando o Projeto com Docker Compose
Para desenvolvimento local, a forma mais simples e prática de executar este projeto é usando o Docker Compose. Ele orquestra todos os serviços necessários (a aplicação e o banco de dados) com um único comando, criando um ambiente consistente e isolado.

Por que usar Docker Compose?
Simplicidade: Inicia toda a aplicação com um comando.

Consistência: Garante que todos os desenvolvedores rodem o projeto com as mesmas configurações.

Isolamento: Evita conflitos de versão de Python, bibliotecas ou do banco de dados com outros projetos na sua máquina.

Guia de Execução
1. Crie o arquivo docker-compose.yml
Na raiz do seu projeto, crie um arquivo chamado docker-compose.yml com o seguinte conteúdo. Ele "traduz" a lógica do ambiente de produção (Kubernetes) para um formato ideal para desenvolvimento.
````
# Arquivo para orquestrar os containers da aplicação e do banco de dados localmente.
version: '3.8'

services:
  # Serviço da aplicação web Flask
  fakeshop:
    build: . # Constrói a imagem a partir do Dockerfile na pasta atual
    container_name: fakeshop_app
    ports:
      - "5000:5000" # Mapeia a porta 5000 do container para a sua máquina
    environment:
      # Variáveis de ambiente que a aplicação precisa para conectar ao banco
      - DB_HOST=postgre
      - DB_USER=fakeshop
      - DB_PASSWORD=Pg1234
      - DB_NAME=fakeshop
      - FLASK_APP=index.py
    depends_on:
      - postgre # Garante que o banco de dados inicie antes da aplicação

  # Serviço do banco de dados PostgreSQL
  postgre:
    image: postgres:13.6
    container_name: postgre_db
    environment:
      # Credenciais para o banco de dados ser criado na inicialização
      - POSTGRES_DB=fakeshop
      - POSTGRES_USER=fakeshop
      - POSTGRES_PASSWORD=Pg1234
    volumes:
      - postgres_data:/var/lib/postgresql/data # Garante que os dados do banco não se percam
    ports:
      - "5432:5432" # Expõe a porta do banco, se precisar acessá-lo diretamente

# Volume para persistir os dados do banco de dados
volumes:
  postgres_data:
````
2. Inicie a Aplicação
Abra um terminal na raiz do projeto e execute:
````
docker-compose up --build
````
O que este comando faz?

up: Inicia os serviços (fakeshop e postgre).

--build: Força a reconstrução da imagem da sua aplicação. É importante usar esta flag sempre que você fizer alterações no código ou no Dockerfile.

3. Acesse a Aplicação
Pronto! Abra seu navegador e acesse http://localhost:5000.

Comandos Úteis
Para parar tudo:
````
# Para os containers e remove a rede criada
docker-compose down
````
Para parar e apagar os dados do banco:
````
# CUIDADO: Isso apagará todos os dados salvos no banco de dados.
docker-compose down -v
````
