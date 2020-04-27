---
title: Exibindo e parando os pacotes em execução no servidor de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a53cf3dbd11c87177c725cf246fb4b1016d87ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054595"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Exibindo e parando pacotes que são executados no servidor do Integration Services
  O banco de dados do `SSISDB` armazena o histórico da execução em tabelas internas que não são visíveis aos usuários. Porém, ele expõe as informações necessárias por meio de exibições públicas que você pode consultar. Ele também fornece procedimentos armazenados que você pode chamar para executar tarefas comuns relacionadas a pacotes.  
  
 Normalmente você gerencia objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. No entanto, você também pode consultar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados para executar muitas de suas tarefas. Por exemplo, você pode exibir a lista de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que estão em execução atualmente no servidor e solicitar a interrupção de pacotes, se necessário.  
  
## <a name="viewing-the-list-of-running-packages"></a>Exibindo a lista de pacotes em execução  
 É possível exibir a lista de pacotes que estão sendo executados no momento no servidor na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir a lista de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] acesso  
 Para exibir a lista de pacotes em execução no servidor, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) para obter pacotes que têm um status 2.  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="stopping-a-running-package"></a>Interrompendo um pacote em execução  
 Você pode solicitar um pacote em execução a ser interrompido na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para interromper um pacote em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] acesso  
 Para interromper um pacote em execução no servidor, chame o procedimento armazenado, [catalog.stop_operation &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>Exibindo o histórico de pacotes executados  
 Para exibir o histórico de pacotes executados no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], use o relatório **Todas as Execuções** . Para obter mais informações sobre o relatório **Todas as Execuções** e outros relatórios padrão, consulte [Relatórios do servidor do Integration Services](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir o histórico de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] acesso  
 Para exibir informações sobre os pacotes que foram executados, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)   
 [Solucionando problemas de relatórios para execução de pacotes](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  
