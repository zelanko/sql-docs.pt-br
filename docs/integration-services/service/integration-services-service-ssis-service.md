---
title: "Servi&#231;o do Integration Services (Servi&#231;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "serviço Integration Services, sobre o serviço Integration Services"
  - "serviço do SQL Server Integration Services"
  - "serviço [Integration Services], sobre o serviço Integration Services"
  - "serviço [Integration Services]"
  - "SQL Server Integration Services, serviço"
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Servi&#231;o do Integration Services (Servi&#231;o SSIS)
  Os tópicos desta seção discutem o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um serviço do Windows para gerenciamento de pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Este serviço não é exigido para criar, salvar e executar pacotes do Integration Services. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para compatibilidade com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena objetos, configurações e dados operacionais no banco de dados **SSISDB** para projetos que você implantou no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o modelo de implantação de projetos. O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que é uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hospeda o banco de dados. Para obter mais informações sobre o banco de dados, consulte [Catálogo do SSIS](../../integration-services/service/ssis-catalog.md). Para obter mais informações sobre implantação de projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Implantar projetos no servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
## Recursos de gerenciamento  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um serviço Windows para gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está disponível apenas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 A execução do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece os seguintes recursos de gerenciamento:  
  
-   Início dos pacotes armazenados local e remoto  
  
-   Interrupção dos pacotes em execução local e remoto  
  
-   Monitoramento dos pacotes em execução local e remoto.  
  
-   Importação e exportação de pacotes  
  
-   Gerenciamento do armazenamento de pacotes  
  
-   Personalização das pastas de armazenamento  
  
-   Interrupção de pacotes em execução quando o serviço é interrompido  
  
-   Exibição do log de Eventos do Windows  
  
-   Conectar-se a vários servidores [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
## Tipo de inicialização do serviço Integration Services  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado quando você instala o componente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático. O serviço deve estar em execução para monitorar os pacotes armazenados no Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)]. O Repositório de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] pode estar no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou nas pastas designadas no sistema de arquivos.  
  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não será necessário se você só quiser projetar e executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Porém, o serviço é necessário para listar e monitorar pacotes usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## Tarefas relacionadas  
  
-   [Definir as propriedades do serviço do Integration Services](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
-   [Exibir eventos para o serviço do Integration Services](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
  