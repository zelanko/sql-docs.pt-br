---
title: sys.database_event_sessions (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 02c2cd71-d35e-4d4c-b844-92b240f768f4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcfbd264a3ec5d1cd4561fa298ead76a7d66d3b7
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabaseeventsessions-azure-sql-database"></a>sys.database_event_sessions (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Lista todas as definições de sessão de evento que existem no banco de dados atual, em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  A exibição de catálogo semelhante denominada `sys.server_event_sessions` só se aplica ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]e para todas as versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**Int**|A ID exclusiva da sessão de evento. Não permite valor nulo.|  
|name|**sysname**|O nome definido pelo usuário para identificar a sessão de evento. nome é exclusivo. Não permite valor nulo.|  
|event_retention_mode|**nchar(1)**|Determina como a perda de evento é tratada. O padrão é S. Não é anulável. É um dos seguintes:<br /><br /> S. Mapeia para event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS<br /><br /> M. Mapeia para event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS<br /><br /> N. Mapeia para event_retention_mode_desc = NO_EVENT_LOSS|  
|event_retention_mode_desc|**sysname**|Descreve como a perda de evento é tratada. O padrão é ALLOW_SINGLE_EVENT_LOSS. Não permite valor nulo. É um dos seguintes:<br /><br /> ALLOW_SINGLE_EVENT_LOSS. Os eventos podem ser perdidos da sessão. Eventos únicos serão descartados somente quando todos os buffers de evento estiverem cheios. A perda de um único evento quando os buffers de evento estiverem cheios permite características de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitáveis, enquanto minimiza a perda no fluxo de eventos processados.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS. Os buffers de evento cheios podem ser perdidos da sessão. O número de eventos depende do tamanho de memória alocado à sessão, do particionamento da memória e do tamanho dos eventos no buffer. Essa opção minimiza o impacto de desempenho no servidor quando os buffers de evento forem rapidamente cheios. No entanto, números elevados de eventos podem ser perdidos da sessão.<br /><br /> NO_EVENT_LOSS. Nenhuma perda de evento é permitida. Essa opção assegura que todos os eventos gerados serão retidos. Usando essa opção força todas as tarefas que acionam eventos a esperar até que haja espaço disponível em um buffer de evento. Isso pode causar redução no desempenho detectável enquanto a sessão de evento está ativa.|  
|max_dispatch_latency|**Int**|A quantidade de tempo, em milissegundos, em que haverá buffer de eventos na memória antes que sejam entregues para destinos de sessão. Os valores válidos são de 1 a 2147483648 e -1. Um valor de -1 indica que a latência de distribuição é infinita. Permite valor nulo.|  
|max_memory|**Int**|A quantidade de memória alocada à sessão para buffer de evento. O valor padrão é de 4 MB. Permite valor nulo.|  
|max_event_size|**Int**|A quantidade de memória definida separadamente para eventos que não se ajustam em buffers de sessão de evento. Se max_event_size exceder o tamanho do buffer calculado, serão alocados dois buffers adicionais de max_event_size à sessão de evento. Permite valor nulo.|  
|memory_partition_mode|**nchar(1)**|O local na memória no qual são criados buffers de evento. O modo de partição padrão é G. Não é anulável. memory_partition_mode é um de:<br /><br /> G - NONE<br /><br /> C - PER_CPU<br /><br /> N - PER_NODE|  
|memory_partition_mode_desc|**sysname**|O padrão é NONE. Não permite valor nulo. É um dos seguintes:<br /><br /> NONE. Um único conjunto de buffers é criado na instância do SQL Server.<br /><br /> PER_CPU. Um conjunto de buffers é criado para cada CPU.<br /><br /> PER_NODE. Um conjunto de buffers é criado para nó NUMA (acesso de memória não uniforme).|  
|track_causality|**bit**|Habilita ou desabilita o rastreamento de causalidade. Se definido como 1 (ON), o rastreamento será habilitado e eventos relacionados em conexões de servidor diferentes podem ser correlacionados. A configuração padrão é 0 (OFF). Não permite valor nulo.|  
|startup_state|**bit**|O valor determina se a sessão é ou não iniciada automaticamente quando o servidor for iniciado. O padrão é 0. Não permite valor nulo. É um dentre:<br /><br /> 0 (OFF). A sessão não inicia quando o servidor iniciar.<br /><br /> 1 (ON). A sessão de evento inicia quando o servidor iniciar.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
  
