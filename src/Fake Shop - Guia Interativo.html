<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dica Rápida: Rodando o Projeto com Docker Compose</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .code-block {
            background-color: #1f2937; /* bg-gray-800 */
            color: #d1d5db; /* text-gray-300 */
            padding: 1.5rem;
            border-radius: 0.5rem;
            position: relative;
        }
        .code-block-header {
            padding-bottom: 1rem;
            border-bottom: 1px solid #374151; /* border-gray-700 */
            margin-bottom: 1rem;
            font-size: 0.875rem;
            color: #9ca3af; /* text-gray-400 */
        }
        .copy-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background-color: #4b5563; /* bg-gray-600 */
            color: white;
            border: none;
            padding: 0.25rem 0.75rem;
            border-radius: 0.375rem;
            cursor: pointer;
            font-size: 0.875rem;
            transition: background-color 0.2s;
        }
        .copy-btn:hover {
            background-color: #374151; /* bg-gray-700 */
        }
    </style>
</head>
<body class="bg-gray-50">
    <main class="max-w-4xl mx-auto p-4 md:p-8 text-gray-800">

        <h1 class="text-3xl font-bold mb-4">💡 Dica Rápida: Rodando o Projeto com Docker Compose</h1>
        <p class="text-lg text-gray-600 mb-8">
            Para desenvolvimento local, a forma mais simples e prática de executar este projeto é usando o <strong>Docker Compose</strong>. Ele orquestra todos os serviços necessários (a aplicação e o banco de dados) com um único comando, criando um ambiente consistente e isolado.
        </p>

        <h2 class="text-2xl font-bold border-b pb-2 mb-6">Por que usar Docker Compose?</h2>
        <ul class="list-disc list-inside space-y-2 mb-10 text-gray-700">
            <li><strong>Simplicidade:</strong> Inicia toda a aplicação com um comando.</li>
            <li><strong>Consistência:</strong> Garante que todos os desenvolvedores rodem o projeto com as mesmas configurações.</li>
            <li><strong>Isolamento:</strong> Evita conflitos de versão de Python, bibliotecas ou do banco de dados com outros projetos na sua máquina.</li>
        </ul>

        <h2 class="text-2xl font-bold border-b pb-2 mb-6">Guia de Execução</h2>

        <h3 class="text-xl font-semibold mb-3">1. Crie o arquivo `docker-compose.yml`</h3>
        <p class="text-gray-600 mb-4">
            Na raiz do seu projeto, crie um arquivo chamado <code>docker-compose.yml</code> com o seguinte conteúdo. Ele "traduz" a lógica do ambiente de produção (Kubernetes) para um formato ideal para desenvolvimento.
        </p>
        <div class="code-block mb-8">
            <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
            <pre><code># Arquivo para orquestrar os containers da aplicação e do banco de dados localmente.
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
</code></pre>
        </div>

        <h3 class="text-xl font-semibold mb-3">2. Inicie a Aplicação</h3>
        <p class="text-gray-600 mb-4">
            Abra um terminal na raiz do projeto e execute:
        </p>
        <div class="code-block mb-4">
            <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
            <pre><code>docker-compose up --build</code></pre>
        </div>
        <div class="bg-blue-50 border-l-4 border-blue-400 text-blue-800 p-4 mb-8" role="alert">
            <p class="font-bold">O que este comando faz?</p>
            <ul class="list-disc list-inside mt-2">
                <li><strong>up:</strong> Inicia os serviços (<code>fakeshop</code> e <code>postgre</code>).</li>
                <li><strong>--build:</strong> Força a reconstrução da imagem da sua aplicação. É importante usar esta flag sempre que você fizer alterações no código ou no <code>Dockerfile</code>.</li>
            </ul>
        </div>

        <h3 class="text-xl font-semibold mb-3">3. Acesse a Aplicação</h3>
        <p class="text-gray-600 mb-10">
            Pronto! Abra seu navegador e acesse <a href="http://localhost:5000" target="_blank" class="text-blue-600 hover:underline font-medium">http://localhost:5000</a>.
        </p>

        <h2 class="text-2xl font-bold border-b pb-2 mb-6">Comandos Úteis</h2>
        
        <h4 class="font-semibold mb-2">Para parar tudo:</h4>
        <div class="code-block mb-6">
            <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
            <pre><code># Para os containers e remove a rede criada
docker-compose down</code></pre>
        </div>

        <h4 class="font-semibold mb-2">Para parar e apagar os dados do banco:</h4>
        <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
            <pre><code># CUIDADO: Isso apagará todos os dados salvos no banco de dados.
docker-compose down -v</code></pre>
        </div>

    </main>

    <script>
        function copyCode(buttonElement) {
            const pre = buttonElement.nextElementSibling;
            const code = pre.querySelector('code');
            const textToCopy = code.innerText;
            
            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = textToCopy;
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextArea);

            const originalText = buttonElement.innerText;
            buttonElement.innerText = 'Copiado!';
            buttonElement.style.backgroundColor = '#22c55e'; // green-500
            setTimeout(() => {
                buttonElement.innerText = originalText;
                buttonElement.style.backgroundColor = '#4b5563'; // bg-gray-600
            }, 2000);
        }
    </script>

</body>
</html>
