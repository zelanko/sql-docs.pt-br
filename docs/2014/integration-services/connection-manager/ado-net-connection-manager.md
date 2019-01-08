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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c58df877a98ac5c62aeb7d7ca45beed7f129eaf0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799808"
---
# <a name="adonet-connection-manager"></a>Gerenciador de conexões ADO.NET
  Um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite que um pacote acesse fontes de dados usando um provedor .NET. Esse gerenciador de conexões é geralmente usado para acessar fontes de dados como do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e também fontes de dados exibidas pelo OLE DB e XML em tarefas personalizadas, gravadas em códigos gerenciados e usando uma linguagem C#.  
  
 Quando você adiciona uma [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão a um pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão manager é resolvido como um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] conexão em tempo de execução, define propriedades do Gerenciador da conexão e adiciona o Gerenciador de conexão o `Connections` coleção do pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `ADO.NET`. O valor de `ConnectionManagerType` está qualificado para incluir o nome do provedor .NET usado pelo gerenciador de conexões.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solução de problemas do gerenciador de conexões ADO.NET  
 Você pode registrar as chamadas que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz a provedores de dados externos. Você pode usar esse recurso de registro para solucionar problemas de conexões que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz com fontes de dados externas. Para registrar as chamadas que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz aos provedores de dados externos, habilite o registro do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Ao serem lidos por um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , os dados de certos tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vão gerar os resultados mostrados na tabela a seguir.  
  
|Tipo de dados do SQL Server|Resultado|  
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
  
## <a name="see-also"></a>Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
