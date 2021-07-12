[![Build status](https://dev.azure.com/natan-dias/Desafio%20-%20Agility/_apis/build/status/Desafio%20-%20Agility-Docker)](https://dev.azure.com/natan-dias/Desafio%20-%20Agility/_build/latest?definitionId=10) ![Release](https://vsrm.dev.azure.com/natan-dias/_apis/public/Release/badge/5d37c8e4-0faf-40c6-85d6-df1c129089a1/1/1)

# Desafio Agility

Exercício para avaliação do desafio proposto pela Agility.

## Recursos utilizados:

+ Azure DevOps - Build e Release
+ Azure Web App Service
+ Azure Repo

## Building

Criação de duas Pipelines para Build. A pipeline ativa foi criada com o editor clássico e a inativa está configurada com arquivo YAML.

O objetivo da Pipeline é o build da imagem docker e push para o meu repositório no Docker Hub. Escolhi este método para poupar recursos utilizados em minha conta na Azure, porém o push pode ser feito para o Azure Container Registry sem nenhum problema.

![image.png](/.attachments/image-aa0f5135-290d-4f2d-bf3a-8ed1ed8c3226.png)

Adicionado as tags conforme na imagem para que o push sempre utilize o número da build como tag da imagem Docker e também sempre adicione as novas imagens com a tag "latest" para facilitar a configuração do release e futuras atualizações da aplicação no Azure.

Habilitado também a Integração Contínua (não necessário se utilizar o YAML) para que o build ocorra sempre que um commit for realizado no repositório.

Repositório Docker com a imagem após a build:

> docker.io/natandias1/docker-pets

## Release

Criado uma pipeline de Release para update do App na Azure sempre que a build for realizada, também com a Integração Contínua habilitada. O build gera um artefato e o release entrega a atualização para o Azure App Service.

O release precisa ter configurado:

+ Nome do serviço no Azure
+ Nome do repositório e tag

A pipeline de release necessita de aprovação, apenas como forma de demonstrar o conceito de aprovação antes do deployment em produção.

## Azure Web App

No Azure foi criado um Web App Container Service, com um link para o repositório no Docker Hub. Semṕre que a imagem é atualizada pela build, o release também acontece com a atualização no Azure Web App Service para que a aplicação utilize a nova imagem atualizada do registry.

![image.png](/.attachments/image-43f85ce0-b0d5-40ed-8f19-6144bf26fa91.png)

## Aplicação

A aplicação está publicada na URL:

> https://docker-pets.azurewebsites.net/

Repositório da aplicação:

> https://github.com/natan-dias/docker-pets

