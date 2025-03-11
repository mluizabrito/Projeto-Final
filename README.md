# Projeto Final Da Turma de NOV_2024 
Projeto Cloud AWS - Trilha DevSecOps do programa de bolsas da empresa compass.uol 

## 👥 Dupla
- Maria Luiza Nascimento De Brito Araújo
- Matheus De Miranda Mendonça

## 💡 Case - Problema a ser solucionado

Nós somos da empresa "Fast Engineering S/A" e gostaríamos de uma solução dos senhores(as), que fazem parte da empresa terceira "TI SOLUÇÕES INCRÍVEIS". Nosso eCommerce está crescendo e a solução atual não está atendendo mais a alta demanda de acessos e compras que estamos tendo. 

## 🎯 Objetivos principais
- Realizar a migração do ambiente abaixo para AWS, seguindo as melhores práticas da arquitetura em Cloud AWS

![ARQUITETURA](Diagramas/ambienteAtual.JPG)

## 	:mag_right: ÍNDICE
1. [Lift and Shift](#1-Lift-and-Shift)
* [Atividades necessárias](#11-atividades-necessárias)
* [Ferramentas utilizadas](#12-ferramentas-utilizadas)
* [Diagrama As-Is](#13-diagrama-lift-and-shift)
* [Segurança](#14-segurança)
* [Backup](#15-backup)
* [Custo da Infraestrutura](#16-aws-pricing)
2. [Modernizacao com EKS (Elastic Kubernetes Service)](#2-kubenets)
*  [Atividades necessárias](#21-atividades-necessárias)
* [Ferramentas utilizadas](#22-ferramentas-utilizadas)
* [Diagrama](#23-diagrama-kubernets)
* [Segurança](#24-segurança)
* [Backup](#25-backup)
* [Custo da Infraestrutura](#26-aws-pricing)

## 1. Lift and Shift
Lift and shift, também conhecida como “rehosting” consiste em migrar uma aplicação de um ambiente para outro, sem grandes mudanças. No projeto, o ambiente on-premises da empresa "Fast Engineering S/A" vai ser migrado para a AWS.

## 1.1 Atividades necessárias
- Analisar a Infraestrutura atual

- Migração do Banco de Dados
    - Criar e configurar Amazon RDS para MySQL
    - Configuração do Amazon DMS (Database Migration Service)

- Migração do Frontend e backend
    - Instale o Replication Agent no servidor.
    - Configure o Amazon MGN para replicar o servidor para a AWS.
    - Configure EC2 e o armazenamento de objetos
    - Criar e configurar Amazon S3 para armazenamento de estáticos
    - Fazer upload dos arquivos do React para o bucket S3
    - Criar e configurar um CloudFront para o bucket
    - Configurar DNS

- Preparação do ambiente na AWS:
    - Configurar networking -> VPC para isolar os recursos
    - Configurar security groups para controle de tráfego
    - Configurar IAM para controlar o acesso aos recursos da AWS

-  Finalizar a migração => Corte
    - Atualize o registro do DNS
    - Realize o Backup completo do ambiente on-premises antes de desativá-lo
    - Monitoramento com CloudWatch
    - Desative os servidores antigos

### 1.2 Ferramentas utilizadas

- AWS MGN (Application Migration Service) -> Serviço da Amazon para automatizar a migração Lift and Shift de servidores. Documentação: https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html
- AWS DMS (Database Migration Service) -> Utilizado para migrar dados em um banco on-premises para o RDS. Documentação: https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html
- AWS RDS (Relational Database Service) -> Banco de dados relacional de gerenciamento fácil. Documentação: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
- Amazon EC2 (Elastic Compute Cloud ) -> Disponibiliza o acesso sob demanda e escalável de capacidade de computação, reduzindo os custos com hardware. Documentação: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html
- AWS S3 ( Amazon Simple Storage Service) -> Serviço de armazenamento de objetos. Documentação: https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- Amazon CloudFront -> Acelera a distribuição de arquivos estáticos. Documentação: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html
- Amazon CloudWatch -> Monitoramento recursos e as aplicações em tempo real na infraestrutura AWS. Documentação: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.ht
- Amazon Backup -> Permite configurar políticas de backup e monitorar a atividade de recursos na AWS. Documentação: https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html
- Amazon VPC (Virtual private cloud) -> Utilizada para isolamento e segurança de rede, semelhante a rede tradicional. Documentação: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
- IAM (AWS  Identity and Access Management ) -> É um serviço que permite gerenciar usuários, credenciais de segurança que controlam quais usuário e aplicações podem acessar os recursos da AWS. Documentação: https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
- Security Groups -> Configuração de segurança e controle de acesso.
- AWS Pricing Calculator -> Ferramenta da AWS Billing and Cost Management que permite estimar os custos da arquitetura. Documentação: https://docs.aws.amazon.com/cost-management/latest/userguide/pricing-calculator.html

### 1.3 Diagrama Lift and Shift


### 1.4 Segurança

- VPC com subnet privadas e pública
- Banco de dados - RDS em subnet privada
- Security group limitando o tráfego
- IAM para limitar acesso aos recursos da AWS
- Criptografia em repouso KMS para RDS e SSE-S3 (Sem custo adicional) para Amazon S3
    - Criptografia em trânsito TLS para RDS e HTTPS para S3

### 1.5 Backup
- AWS backups para EC2
- RDS ->backups automatizados
- S3 -> Replication/Versionamento + Ciclo de Vida do S3/Lifecycle Policy

### 1.6 Custo de infraestrutura

![CUSTO](Diagramas/custoAsIS.JPG)

Para visualizar informações detalhadas sobre a estimativa clique [aqui](https://github.com/mluizabrito/Projeto-Final/blob/main/Aws%20Pricing/custoAws.pdf)

### 2. Modernizacao com EKS (Elastic Kubernetes Service):

# Objetivos

Queremos modernizar esse sistema para **AWS**, seguindo as **melhores práticas de arquitetura em Cloud AWS**.  

A nova arquitetura deve seguir as seguintes diretrizes:

- **Alta disponibilidade**: Garantir que o sistema esteja sempre acessível, utilizando múltiplas zonas de disponibilidade (AZs).
- **Escalabilidade**: Permitir crescimento automático da infraestrutura conforme a demanda.
- **Segurança**: Aplicar boas práticas de segurança, como **IAM**, **VPCs privadas**, **WAF** e **criptografia** de dados.
- **Custo-efetividade**: Utilizar serviços gerenciados para otimizar custos operacionais.
- **Monitoramento e Logging**: Implementar **CloudWatch**, **AWS Config** e **GuardDuty** para auditoria e detecção de anomalias.
- **Automação e Infraestrutura como Código**: Provisionar recursos usando **Terraform** ou **AWS CloudFormation**.


### 2.1 Atividades necessárias

### 2.2 Ferramentas utilizadas

### 2.3 Diagrama Kubernets

### 2.4 Segurança

# Monitoramento e Segurança na AWS

## CloudWatch Logs e Metrics

- Instalar o **CloudWatch Agent** ou ativar **Container Insights** para coletar logs e métricas dos pods.
- Criar **alarmes no CloudWatch** para eventos como:
  - Alto uso de CPU e memória.
  - Erros **5xx** no **ALB** (Application Load Balancer).

## WAF + CloudFront

- Utilizar o **CloudFront** como **CDN** para conteúdo estático e cache global.
- Ativar **AWS WAF** para proteger contra ataques de camada 7, como:
  - **SQL Injection (SQLi)**
  - **Cross-Site Scripting (XSS)**

## IAM Roles e KMS

- Aplicar o **princípio de menor privilégio** para acesso a recursos.
- **Criptografar** dados sensíveis utilizando **AWS KMS**.

## GuardDuty e AWS Config (Opcional)

- **Monitorar ameaças e conformidade** com **AWS GuardDuty** e **AWS Config**.
- Configurar **alertas** para:
  - Acessos suspeitos.
  - Configurações inadequadas.

---
 **Recomendações**  
Para garantir a segurança e o monitoramento adequado, revise as permissões IAM regularmente e implemente logs centralizados para auditoria.


### 2.5 Backup

### 2.6 AWS Pricing 

