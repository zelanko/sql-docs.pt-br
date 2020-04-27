---
title: Gerenciador de Conexões ADO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7fda014196d933ef9d5391ab4db798d821e43610
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833782"
---
# <a name="ado-connection-manager"></a>Gerenciador de conexões ADO
  Um gerenciador de conexões ADO permite a um pacote se conectar a ActiveX Data Objects (ADO), como um conjunto de registros. Este gerenciador de conexões é usado tipicamente em tarefas personalizadas escritas em uma versão anterior da linguagem, como o Microsoft Visual Basic 6.0, ou em tarefas personalizadas que são parte de uma aplicação existente que usa ADO para conectar em uma fonte de dados.  
  
 Quando você adiciona um Gerenciador de conexões ADO a um pacote [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o cria um Gerenciador de conexões que será resolvido para uma conexão ADO em tempo de execução, define as propriedades do Gerenciador de conexões e adiciona `Connections` o Gerenciador de conexões à coleção no pacote. A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `ADO`.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>Solucionando problemas do gerenciador de conexões ADO  
 Ao serem lidos por um gerenciador de conexões ADO, certos tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vão gerar os resultados mostrados na tabela a seguir.  
  
|Tipos de dados do SQL Server|Result|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|O pacote apresentará erros, a menos que use comandos com parâmetros SQL. Para utilizar comandos SQL parametrizados, use a tarefa Executar SQL em seu pacote. Para obter mais informações, consulte [Tarefa Executar SQL](../control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../parameters-and-return-codes-in-the-execute-sql-task.md).|  
|`datetime2`|O gerenciador de conexões ADO trunca o valor de milissegundo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="configuring-the-ado-connection-manager"></a>Configurando o gerenciador de conexões ADO  
 Você pode configurar um gerenciador de conexões ADO das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.  
  
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.  
  
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Configurar Gerenciador de Conexões OLE DB](ole-db-connection-manager.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
