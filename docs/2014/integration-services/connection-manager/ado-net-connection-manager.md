---
title: Gerenciador de Conexões ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 97a0690775b7b6d95a257bc5f5ed0a6483e1c24a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833858"
---
# <a name="adonet-connection-manager"></a>Gerenciador de conexões ADO.NET
  Um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite que um pacote acesse fontes de dados usando um provedor .NET. Esse gerenciador de conexões normalmente é usado para acessar fontes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de dados, como e também fontes de dados expostas por meio de OLE DB e XML em tarefas personalizadas que são escritas em código gerenciado usando uma linguagem como C#.  
  
 Quando você adiciona um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexões a um pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o cria um Gerenciador de conexões que é [!INCLUDE[vstecado](../../includes/vstecado-md.md)] resolvido como uma conexão em tempo de execução, define as propriedades do Gerenciador de conexões e adiciona `Connections` o Gerenciador de conexões à coleção no pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `ADO.NET`. O valor de `ConnectionManagerType` está qualificado para incluir o nome do provedor .NET usado pelo gerenciador de conexões.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solução de problemas do gerenciador de conexões ADO.NET  
 Você pode registrar as chamadas que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz a provedores de dados externos. Você pode usar esse recurso de registro para solucionar problemas de conexões que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz com fontes de dados externas. Para registrar as chamadas que o [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexões faz aos provedores de dados externos, habilite o log de pacote e selecione o evento de **diagnóstico** no nível do pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Ao serem lidos por um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , os dados de certos tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vão gerar os resultados mostrados na tabela a seguir.  
  
|Tipo de dados do SQL Server|Result|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|O pacote apresentará erros, a menos que use comandos com parâmetros SQL. Para utilizar comandos SQL parametrizados, use a tarefa Executar SQL em seu pacote. Para obter mais informações, consulte [Tarefa Executar SQL](../control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../parameters-and-return-codes-in-the-execute-sql-task.md).|  
|`datetime2`|O gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] trunca o valor de milissegundo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configuração do gerenciador de conexões ADO.NET  
 Você pode configurar um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] das seguintes formas:  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor .NET selecionado.  
  
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.  
  
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Muitas das opções de configuração do gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dependem do provedor .NET que o gerenciador de conexões usa.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , clique em um dos seguintes tópicos:  
  
-   [Configurar Gerenciador de Conexões ADO.NET](../configure-ado-net-connection-manager.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
