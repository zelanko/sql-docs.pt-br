---
title: "Gerenciador de Conexão ADO | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b42410ae3654bed35103ea9b0dcafedff32e3af7
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="ado-connection-manager"></a>Gerenciador de conexões ADO
  Um gerenciador de conexões ADO permite a um pacote se conectar a ActiveX Data Objects (ADO), como um conjunto de registros. Este gerenciador de conexões é usado tipicamente em tarefas personalizadas escritas em uma versão anterior da linguagem, como o Microsoft Visual Basic 6.0, ou em tarefas personalizadas que são parte de uma aplicação existente que usa ADO para conectar em uma fonte de dados.  
  
 Ao adicionar um gerenciador de conexões ADO a um pacote, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que será resolvido para uma conexão ADO em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **ADO**.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>Solucionando problemas do gerenciador de conexões ADO  
 Ao serem lidos por um gerenciador de conexões ADO, certos tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vão gerar os resultados mostrados na tabela a seguir.  
  
|Tipos de dados do SQL Server|Resultado|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|O pacote apresentará erros, a menos que use comandos com parâmetros SQL. Para utilizar comandos SQL parametrizados, use a tarefa Executar SQL em seu pacote. Para obter mais informações, consulte [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|O gerenciador de conexões ADO trunca o valor de milissegundo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="configuring-the-ado-connection-manager"></a>Configurando o gerenciador de conexões ADO  
 Você pode configurar um gerenciador de conexões ADO das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.  
  
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.  
  
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  

