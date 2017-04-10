---
title: "Exibindo e parando pacotes que s&#227;o executados no servidor do Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes [Integration Services], gerenciando"
  - "gerenciando pacotes em execução [Integration Services]"
  - "pacotes [Integration Services], executando"
  - "pacote em execução [Integration Services], gerenciando"
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Exibindo e parando pacotes que s&#227;o executados no servidor do Integration Services
  O banco de dados do **SSISDB** armazena o histórico da execução em tabelas internas que não são visíveis aos usuários. Porém, ele expõe as informações necessárias por meio de exibições públicas que você pode consultar. Ele também fornece procedimentos armazenados que você pode chamar para executar tarefas comuns relacionadas a pacotes.  
  
 Normalmente você gerencia objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, você também pode consultar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados para executar muitas de suas tarefas. Por exemplo, você pode exibir a lista de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que estão em execução atualmente no servidor e solicitar a interrupção de pacotes, se necessário.  
  
## Exibindo a lista de pacotes em execução  
 É possível exibir a lista de pacotes que estão sendo executados no momento no servidor na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir a lista de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para exibir a lista de pacotes em execução no servidor, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) para obter pacotes que têm um status 2.  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## Interrompendo um pacote em execução  
 Você pode solicitar um pacote em execução a ser interrompido na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para interromper um pacote em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para interromper um pacote em execução no servidor, chame o procedimento armazenado, [catalog.stop_operation &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## Exibindo o histórico de pacotes executados  
 Para exibir o histórico de pacotes executados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use o relatório **Todas as Execuções** . Para obter mais informações sobre o relatório **Todas as Execuções** e outros relatórios padrão, consulte [Relatórios do servidor do Integration Services](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir o histórico de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para exibir informações sobre os pacotes que foram executados, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## Consulte também  
 [Execução de projetos e pacotes](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Solucionando problemas de relatórios para execução de pacotes](https://msdn.microsoft.com/library/gg471512.aspx)  
  
  