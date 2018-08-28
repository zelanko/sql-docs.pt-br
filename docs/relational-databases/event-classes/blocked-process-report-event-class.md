---
title: Classe de evento Blocked Process Report | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Blocked Process Report event class
ms.assetid: e8acb408-938d-4b36-81dd-04f087410cc5
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6152a6d0772d67fc72cb4c563bb6e37e61007cb
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063753"
---
# <a name="blocked-process-report-event-class"></a>classe de evento Blocked Process Report
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento **Blocked Process Report** indica que uma tarefa foi bloqueada por um período mais longo que o especificado. Essa classe de evento não inclui tarefas de sistema ou tarefas que estejam esperando em recursos não detectáveis por deadlock.  
  
 Para configurar o limite e a frequência de geração dos relatórios, use o comando **sp_configure** para configurar a opção **blocked process threshold** , que pode ser definida em segundos. Por padrão, não são produzidos relatórios de processo bloqueado. Para obter mais informações sobre como configurar a opção **blocked process threshold**, veja [Opção blocked process threshold de configuração de servidor](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md).  
  
 Para obter informações sobre como filtrar os dados retornados pela classe de evento **Blocked Process Report**, veja [Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md), [Definir um filtro de rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) ou [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md).  
  
## <a name="blocked-process-report-event-class-data-columns"></a>Colunas de dados da classe de evento Blocked Process Report  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID do banco de dados no qual foi adquirido o bloqueio. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**Duration**|**bigint**|O intervalo de tempo (em milissegundos) que o processo ficou bloqueado.|13|Sim|  
|**EndTime**|**datetime**|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como **SQL:BatchStarting** ou **SP:Starting**.|15|Sim|  
|**EventClass**|**int**|Tipo de evento = 137.|27|não|  
|**EventSequence**|**int**|A sequência de determinado evento dentro da solicitação.|51|não|  
|**IndexID**|**int**|ID do índice no objeto afetado pelo evento. Para determinar a ID do índice de um objeto, use a coluna **indid** da tabela do sistema **sysindexes** .|24|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginSid**|**imagem**|SID (identificador de segurança) do usuário que fez logon. Esse evento sempre é informado pelo thread do sistema. IsSystem = 1; SID = sa.|41|Sim|  
|**Modo**|**int**|O estado que o evento recebeu ou que está solicitando.<br /><br /> 0= NULL<br /><br /> 1=Sch-S<br /><br /> 2=Sch-M<br /><br /> 3=S<br /><br /> 4=U<br /><br /> 5=X<br /><br /> 6=IS<br /><br /> 7=IU<br /><br /> 8=IX<br /><br /> 9=SIU<br /><br /> 10=SIX<br /><br /> 11=UIX<br /><br /> 12=BU<br /><br /> 13=RangeS-S<br /><br /> 14=RangeS-U<br /><br /> 15=RangeI-N<br /><br /> 16=RangeI-S<br /><br /> 17=RangeI-U<br /><br /> 18=RangeI-X<br /><br /> 19=RangeX-S<br /><br /> 20=RangeX-U<br /><br /> 21=RangeX-X|32|Sim|  
|**ObjectID**|**int**|A ID atribuída pelo sistema, do objeto em que foi adquirido o bloqueio, se disponível e aplicável.|22|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26||  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao SQL Server usando Login1 e executar uma instrução como Login2, **SessionLoginName** mostrará Login1, enquanto que **LoginName** mostrará Login2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**TextData**|**ntext**|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
