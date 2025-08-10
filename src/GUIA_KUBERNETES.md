Guia de Deploy no Kubernetes com Build Local
Este guia explica como implantar a aplicação "Fake Shop" em um cluster Kubernetes local, construindo a imagem Docker diretamente do seu código-fonte, sem a necessidade de publicá-la em um registro como o Docker Hub.

🚀 Opção: Rodando com Kubernetes (Build Local)
Este método é ideal para testar o ambiente de produção com o código mais recente do seu repositório.

Pré-requisitos
Para seguir este guia, você precisará das seguintes ferramentas instaladas e configuradas em sua máquina:

Git: Para clonar o repositório.

Docker: Para construir a imagem da aplicação.

kubectl: A ferramenta de linha de comando para interagir com o cluster Kubernetes. Instruções de instalação aqui.

Cluster Kubernetes Local: O Kubernetes precisa estar rodando localmente. As opções mais comuns são:

Minikube: Uma ferramenta que cria um cluster Kubernetes de nó único dentro de uma máquina virtual. Guia de instalação do Minikube.

Docker Desktop: Permite habilitar um cluster Kubernetes de nó único diretamente nas configurações (Settings > Kubernetes > Enable Kubernetes). É uma das formas mais simples de começar. Guia do Docker Desktop.

Passo a Passo
1. Clone o Repositório
Primeiro, baixe o código-fonte do projeto para a sua máquina.
````
git clone <URL_DO_SEU_REPOSITORIO_NO_GITHUB>
cd <NOME_DA_PASTA_DO_PROJETO>
````
2. Construa a Imagem Docker
Navegue até a raiz do projeto (onde o Dockerfile está localizado) e construa a imagem. Vamos chamá-la de fakeshop com a tag latest.
````
docker build -t fakeshop:latest .
````
Após a execução, você pode verificar se a imagem foi criada com o comando docker images.

3. Carregue a Imagem no seu Cluster Kubernetes
O Kubernetes precisa ter acesso à imagem que você acabou de construir.

Se você usa Minikube:
Execute o comando abaixo para carregar a imagem fakeshop:latest para dentro do ambiente do Minikube.
````
minikube image load fakeshop:latest
````
Se você usa Docker Desktop:
O Kubernetes do Docker Desktop compartilha o mesmo repositório de imagens do Docker. Nenhum passo adicional é necessário.

4. Atualize o Arquivo deployment.yaml
Agora, precisamos dizer ao Kubernetes para usar a imagem local que acabamos de construir, em vez de tentar baixá-la da internet.

Abra o seu arquivo k8s/deployment.yaml e localize a seção de deployment da aplicação fakeshop. Faça duas alterações:

Altere o campo image para o nome que demos à nossa imagem local: fakeshop:latest.

Adicione o campo imagePullPolicy: IfNotPresent. Isso é crucial e força o Kubernetes a usar a imagem local se ela já existir no cluster.

Antes:

      ...
      containers:
      - name: fakeshop
        image: silvio69luiz/fakeshop:v1
      ...

Depois:

      ...
      containers:
      - name: fakeshop
        image: fakeshop:latest
        imagePullPolicy: IfNotPresent # <-- Adicione esta linha!
      ...

5. Aplique a Configuração no Kubernetes
Com o arquivo deployment.yaml salvo, aplique a configuração no seu cluster.
````
kubectl apply -f k8s/deployment.yaml
````
6. Verifique e Acesse a Aplicação
Espere alguns instantes para os containers iniciarem e, em seguida, verifique o status.

# Deve mostrar os pods 'postgre' e 'fakeshop' com o status 'Running'
````
kubectl get pods
````
# Mostra o serviço 'fakeshop' e como ele está exposto
````]
kubectl get services
````
Para acessar a aplicação:

Se você usa Minikube:
````
minikube service fakeshop
````
Este comando abrirá a URL da aplicação diretamente no seu navegador.

Se você usa Docker Desktop:
O serviço fakeshop estará acessível em http://localhost. Como o Service é do tipo LoadBalancer, o Docker Desktop o expõe na porta 80 por padrão.
