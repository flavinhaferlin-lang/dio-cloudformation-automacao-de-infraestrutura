Implementando Infraestrutura Automatizada com AWS CloudFormation
🧩 Descrição do Projeto

Este projeto faz parte do desafio da DIO (Digital Innovation One), com o objetivo de implementar uma infraestrutura automatizada utilizando o AWS CloudFormation.
A proposta é aplicar na prática os conceitos de Infraestrutura como Código (IaC), documentar todo o processo e organizar um repositório técnico que possa servir de referência para futuros estudos e implementações.

O template desenvolvido cria uma Stack contendo:

Um bucket S3 (com versionamento habilitado);

Um tópico SNS (para notificações);

Saídas automáticas com o nome do bucket e o ARN do tópico.

🎯 Objetivos de Aprendizagem

Ao concluir este projeto, foi possível:

Aplicar conceitos de CloudFormation para criação e gerenciamento automatizado de recursos na AWS;

Documentar de forma estruturada os processos técnicos realizados;

Utilizar o GitHub como ferramenta de versionamento e compartilhamento de documentação técnica;

Compreender melhor a diferença entre CloudFormation e outras ferramentas como o Terraform.

🧱 Estrutura do Repositório
dio-cloudformation-automacao-de-infraestrutura/
├─ README.md
├─ template/
│  └─ cloudformation-template.yaml
├─ images/
│  └─ evidencias.png
└─ docs/
   └─ anotacoes.md (opcional)
   
⚙️ Template CloudFormation (YAML)

Arquivo localizado em: template/cloudformation-template.yaml

AWSTemplateFormatVersion: '2010-09-09'
Description: >
  Template de exemplo para o desafio DIO — cria um bucket S3 e um tópico SNS.

Parameters:
  BucketName:
    Type: String
    Description: Nome do bucket S3 (único globalmente)
    Default: dio-cloudformation-exemplo-${AWS::AccountId}

Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Ref BucketName
      AccessControl: Private
      VersioningConfiguration:
        Status: Enabled
      Tags:
        - Key: Project
          Value: DIO-CloudFormation

  MyTopic:
    Type: AWS::SNS::Topic
    Properties:
      DisplayName: DIO-CloudFormation-Topic
      TopicName: dio-cloudformation-topic

Outputs:
  S3BucketName:
    Description: Nome do bucket S3 criado
    Value: !Ref MyS3Bucket

  SnsTopicArn:
    Description: ARN do tópico SNS criado
    Value: !Ref MyTopic
    
🚀 Passo a Passo de Implementação
1️⃣ Validar o Template

Antes de criar a stack, valide o arquivo YAML para garantir que está correto:

aws cloudformation validate-template --template-body file://template/cloudformation-template.yaml

2️⃣ Criar a Stack

Execute o comando abaixo para criar a infraestrutura:

aws cloudformation create-stack \
  --stack-name dio-cloudformation-exemplo \
  --template-body file://template/cloudformation-template.yaml \
  --parameters ParameterKey=BucketName,ParameterValue=meu-bucket-dio-123456 \
  --capabilities CAPABILITY_NAMED_IAM
  
3️⃣ Acompanhar a Criação da Stack

aws cloudformation describe-stacks --stack-name dio-cloudformation-exemplo

4️⃣ Verificar Recursos Criados

No console da AWS:

Vá até o serviço S3 → veja o bucket criado.
Vá até o SNS → confira o tópico gerado.

5️⃣ Excluir a Stack (quando terminar os testes)

aws cloudformation delete-stack --stack-name dio-cloudformation-exemplo

🧠 Principais Aprendizados

Durante a execução deste desafio, foi possível aprender:

Como criar e gerenciar recursos AWS usando CloudFormation em formato YAML;

A importância da automação da infraestrutura para ganho de agilidade e padronização;

Como validar e depurar templates de infraestrutura como código;

Como organizar e documentar um projeto técnico completo usando GitHub.

🛠️ Tecnologias Utilizadas

AWS CloudFormation

Amazon S3

Amazon SNS

AWS CLI

GitHub

Markdown

🖼️ Evidências do Projeto

As imagens mostram a execução prática do laboratório na AWS


📚 Recursos Úteis

Documentação oficial do AWS CloudFormation

GitHub Quick Start

Guia de Markdown no GitHub

✨ Conclusão

Este desafio proporcionou uma experiência prática completa sobre Infraestrutura como Código (IaC) com o AWS CloudFormation.
O processo de criação, validação e documentação reforçou a importância de automatizar infraestruturas de forma segura, reprodutível e versionada — princípios essenciais para o desenvolvimento moderno em nuvem.

Autora: Flávia Cristiane Ferlin
Desafio: Implementando Infraestrutura Automatizada com AWS CloudFormation — DIO / Santander Code Girls 2025
