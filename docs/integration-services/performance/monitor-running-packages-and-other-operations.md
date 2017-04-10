---
title: "Monitorar a execu&#231;&#227;o de pacotes e outras opera&#231;&#245;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Monitorar a execu&#231;&#227;o de pacotes e outras opera&#231;&#245;es
  Você pode monitorar execuções de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , validações de projeto e outras operações usando uma ou mais das ferramentas a seguir. Algumas ferramentas, como toques de dados, estão disponíveis somente para os projetos que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Logs  
  
     Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
-   Relatórios  
  
     Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
-   Exibições  
  
     Para obter mais informações, consulte [Exibições &#40;Catálogo do Integration Services&#41;](../../integration-services/system-views/views-integration-services-catalog.md).  
  
-   Contadores de desempenho  
  
     Para obter mais informações, consulte [Performance Counters](../../integration-services/performance/performance-counters.md).  
  
-   Toques de dados  
  
## Tipos de operação  
 São monitorados vários tipos diferentes de operações no catálogo **SSISDB**, no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cada operação pode ter várias mensagens associadas a ela. Cada mensagem pode ser classificada em um de vários tipos diferentes. Por exemplo, uma mensagem pode ser de tipo Informações, Aviso ou Erro. Para obter a lista completa dos tipos de mensagem, consulte a documentação da exibição [catalog.operation_messages &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) do Transact-SQL. Para ver uma lista completa dos tipos de operação, consulte [catalog.operations &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  
  
 São usados nove tipos de status diferentes para indicar o status de uma operação. Para ver uma lista completa dos tipos de status, consulte a exibição [catalog.operations &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  
  
## Conteúdo relacionado  
 Entrada de blog, [Visão geral da API do T-SQL SSIS](http://go.microsoft.com/fwlink/?LinkId=249051), em blogs.msdn.com.  
  
  