---
title: 'Relatório de andamento: classe de evento de operação de índice online | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 447358a672abb724ad4c120cdebbad633d07a747
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019392"
---
# <a name="progress-report-online-index-operation-event-class"></a>Classe de evento Progress Report: Online Index Operation
  A classe de evento Progress Report: Online Index Operation  indica o progresso de uma operação de construção de índice online enquanto a operação de construção está em execução.  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>Colunas de dados de classe de evento Progress Report: Online Index Operation  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BigintData1|`bigint`|Número de linhas inseridas.|52|Sim|  
|BigintData2|`bigint`|0 = plano em série; caso contrário, ID de thread durante execução paralela.|53|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duração|`bigint`|Período de tempo (em microssegundos) utilizado pelo evento.|13|Sim|  
|EndTime|`datetime`|Hora em que a operação de índice online foi concluída.|15|Sim|  
|EventClass|`int`|Tipo de evento = 190.|27|não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|não|  
|EventSubClass|`int`|Tipo de subclasse de evento.<br /><br /> 1 = Iniciar<br /><br /> 2=Início de execução da etapa 1<br /><br /> 3=Término de execução da etapa 1<br /><br /> 4= Início de execução da etapa 2<br /><br /> 5= Término de execução da etapa 2<br /><br /> 6=Contagem de linhas inseridas<br /><br /> 7=Concluído<br /><br /> A etapa 1 refere-se ao objeto base (índice clusterizado ou heap), ou se a operação de índice envolver somente um índice não clusterizado. A etapa 2 é usada quando uma operação de compilação de índice envolver a recompilação original além de índices não clusterizados adicionais.  Por exemplo, se um objeto tiver um índice clusterizado e vários índices não clusterizados, 'recompilar tudo' recompilará todos os índices. O objeto base (o índice clusterizado) é recompilado na etapa 1 e, em seguida, todos os índices não clusterizados são recompilados na etapa 2.|21|Sim|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IndexID|`int`|ID do índice no objeto afetado pelo evento.|24|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ObjectID|`int`|ID de objeto atribuída pelo sistema.|22|Sim|  
|ObjectName|`nvarchar`|Nome do objeto que está sendo referenciado.|34|Sim|  
|PartitionId|`bigint`|A ID da partição que está sendo construída.|65|Sim|  
|PartitionNumber|`int`|O número ordinário da partição que está sendo construída.|25|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora do início do evento.|14|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
