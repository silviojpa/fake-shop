<!DOCTYPE html>
<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fake Shop - Guia de Deploy</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .code-block {
            background-color: #1f2937;
            color: #d1d5db;
            padding: 1.5rem;
            border-radius: 0.5rem;
            position: relative;
            margin-bottom: 1.5rem;
        }
        .copy-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background-color: #4b5563;
            color: white;
            border: none;
            padding: 0.25rem 0.75rem;
            border-radius: 0.375rem;
            cursor: pointer;
            font-size: 0.875rem;
            transition: all 0.2s;
        }
        .copy-btn:hover {
            background-color: #374151;
        }
        .tab-btn {
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            border: 2px solid transparent;
        }
        .tab-btn.active {
            background-color: white;
            color: #1d4ed8;
            border-color: #e0e7ff;
            box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
        }
        .tab-btn:not(.active) {
            background-color: transparent;
            color: #4b5563;
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
    </style>
</head>
<body class="bg-gray-50">
    <main class="max-w-5xl mx-auto p-4 md:p-8 text-gray-800">

        <section class="text-center mb-12">
            <h1 class="text-4xl font-bold mb-2">Fake Shop - Guia de Deploy</h1>
            <p class="text-lg text-gray-600">Escolha o método de deploy: Docker Compose para desenvolvimento ou Kubernetes para produção.</p>
        </section>

        <div class="bg-gray-100 p-2 rounded-xl mb-8 flex justify-center space-x-2">
            <button id="btn-docker" class="tab-btn active" onclick="showTab('docker')">💻 Docker Compose (Desenvolvimento)</button>
            <button id="btn-k8s" class="tab-btn" onclick="showTab('k8s')">🚀 Kubernetes (Produção)</button>
        </div>

        <!-- Conteúdo do Docker Compose -->
        <div id="content-docker" class="tab-content active">
            <h2 class="text-2xl font-bold border-b pb-2 mb-6">Guia Rápido: Docker Compose</h2>
            <p class="text-gray-600 mb-6">Este método é o mais simples e prático para o desenvolvimento local.</p>

            <h3 class="text-xl font-semibold mb-3">1. Crie o arquivo `docker-compose.yml`</h3>
            <p class="text-gray-600 mb-4">Na raiz do projeto, crie o arquivo com o conteúdo abaixo.</p>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code># docker-compose.yml
version: '3.8'
services:
  fakeshop:
    build: .
    container_name: fakeshop_app
    ports:
      - "5000:5000"
    environment:
      - DB_HOST=postgre
      - DB_USER=fakeshop
      - DB_PASSWORD=Pg1234
      - DB_NAME=fakeshop
    depends_on:
      - postgre
  postgre:
    image: postgres:13.6
    container_name: postgre_db
    environment:
      - POSTGRES_DB=fakeshop
      - POSTGRES_USER=fakeshop
      - POSTGRES_PASSWORD=Pg1234
    volumes:
      - postgres_data:/var/lib/postgresql/data
volumes:
  postgres_data:</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">2. Inicie a Aplicação</h3>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code>docker-compose up --build</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">3. Acesse a Aplicação</h3>
            <p class="text-gray-600">Pronto! Acesse <a href="http://localhost:5000" target="_blank" class="text-blue-600 hover:underline font-medium">http://localhost:5000</a>.</p>
        </div>

        <!-- Conteúdo do Kubernetes -->
        <div id="content-k8s" class="tab-content">
            <h2 class="text-2xl font-bold border-b pb-2 mb-6">Guia de Deploy no Kubernetes com Build Local</h2>
            <p class="text-gray-600 mb-6">Este método simula o ambiente de produção, construindo a imagem localmente.</p>

            <h3 class="text-xl font-semibold mb-3">Pré-requisitos</h3>
            <ul class="list-disc list-inside space-y-2 mb-6 text-gray-700">
                <li><a href="https://git-scm.com/" target="_blank" class="text-blue-600 hover:underline">Git</a></li>
                <li><a href="https://www.docker.com/products/docker-desktop" target="_blank" class="text-blue-600 hover:underline">Docker</a></li>
                <li><a href="https://kubernetes.io/docs/tasks/tools/install-kubectl/" target="_blank" class="text-blue-600 hover:underline">kubectl</a></li>
                <li>Cluster Kubernetes Local (Minikube ou Docker Desktop)</li>
            </ul>

            <h3 class="text-xl font-semibold mb-3">1. Clone o Repositório</h3>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code>git clone &lt;URL_DO_SEU_REPOSITORIO&gt;
cd &lt;NOME_DA_PASTA&gt;</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">2. Construa a Imagem Docker</h3>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code>docker build -t fakeshop:latest .</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">3. Carregue a Imagem no Cluster</h3>
            <p class="text-gray-600 mb-4">Se usar Minikube, execute: <code>minikube image load fakeshop:latest</code>. Se usar Docker Desktop, pule este passo.</p>

            <h3 class="text-xl font-semibold mb-3">4. Atualize o `deployment.yaml`</h3>
            <p class="text-gray-600 mb-4">Em <code>k8s/deployment.yaml</code>, altere a imagem do container `fakeshop` para:</p>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code>      ...
      containers:
      - name: fakeshop
        image: fakeshop:latest
        imagePullPolicy: IfNotPresent # <-- Adicione esta linha!
      ...</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">5. Aplique a Configuração</h3>
            <div class="code-block">
                <button class="copy-btn" onclick="copyCode(this)">Copiar</button>
                <pre><code>kubectl apply -f k8s/deployment.yaml</code></pre>
            </div>

            <h3 class="text-xl font-semibold mb-3">6. Verifique e Acesse</h3>
            <p class="text-gray-600 mb-4">Verifique os pods com <code>kubectl get pods</code>. Para acessar, se usar Minikube, execute <code>minikube service fakeshop</code>. No Docker Desktop, acesse <a href="http://localhost" target="_blank" class="text-blue-600 hover:underline font-medium">http://localhost</a>.</p>
        </div>

    </main>

    <script>
        function showTab(tabName) {
            const contents = document.querySelectorAll('.tab-content');
            contents.forEach(content => {
                content.classList.remove('active');
            });

            const buttons = document.querySelectorAll('.tab-btn');
            buttons.forEach(button => {
                button.classList.remove('active');
            });

            document.getElementById('content-' + tabName).classList.add('active');
            document.getElementById('btn-' + tabName).classList.add('active');
        }

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
            buttonElement.style.backgroundColor = '#22c55e';
            setTimeout(() => {
                buttonElement.innerText = originalText;
                buttonElement.style.backgroundColor = '#4b5563';
            }, 2000);
        }
        
        // Inicia na primeira aba por padrão
        document.addEventListener('DOMContentLoaded', () => {
            showTab('docker');
        });
    </script>

</body>
</html>
