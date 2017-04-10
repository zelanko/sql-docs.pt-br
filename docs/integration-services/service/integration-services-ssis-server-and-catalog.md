---
title: "Integration Services (SSIS) Server e cat&#225;logo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes [Integration Services], gerenciando"
  - "gerenciando pacotes [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Integration Services (SSIS) Server e cat&#225;logo
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o **SSISDB** banco de dados. O banco de dados armazena os seguintes objetos: pacotes, projetos, parâmetros, permissões, propriedades de servidor e histórico operacional.  
  
 O banco de dados do **SSISDB** expõe as informações de objeto em exibições públicas que você pode consultar. O banco de dados também fornece procedimentos armazenados que você pode chamar para gerenciar os objetos.  
  
 Antes de implantar os projetos para o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server, você precisa criar o **SSISDB** catálogo.  
  
 Para obter uma visão geral da funcionalidade do catálogo do SSISDB, consulte [Catálogo do SSIS](../../integration-services/service/ssis-catalog.md).  
  
## Alta disponibilidade  
 Como outros bancos de dados de usuários, o banco de dados **SSISDB** dá suporte a espelhamento de banco de dados e replicação. Para obter mais informações sobre espelhamento e replicação, consulte [espelhamento de banco de dados e 40; SQL Server & 41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Você também pode fornecer alta disponibilidade do SSISDB e seu conteúdo, fazendo uso do SSIS e grupos de disponibilidade AlwaysOn. Para obter mais informações, consulte o blog de Matt Masson, [SSIS com Always On](http://go.microsoft.com/fwlink/?LinkId=255873), em blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor do Integration Services no SQL Server Management Studio  
 Quando você se conectar a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o **SSISDB** banco de dados, consulte os seguintes objetos no Pesquisador de objetos:  
  
-   **Banco de dados SSISDB**  
  
     O banco de dados do **SSISDB** aparece sob o nó **Bancos de Dados** no Pesquisador de Objetos. Você pode consultar as exibições e chamar os procedimentos armazenados que gerenciam o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os objetos que estão armazenados no servidor.  
  
-   **Catálogos do Integration Services**  
  
     No nó **Catálogos do Integration Services** , há pastas para projetos e ambientes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## Tarefas relacionadas  
  
-   [Criar o catálogo do SSIS](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Exibir a lista de pacotes no servidor do Integration Services](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implantar projetos no Servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## Conteúdo relacionado  
 Entrada de blog, [SSIS com Always On](http://go.microsoft.com/fwlink/?LinkId=255873), em blogs.msdn.com.  
  
  