---
description: sys.dm_os_memory_cache_clock_hands (Transact-SQL)
title: sys.dm_os_memory_cache_clock_hands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb93ff8ecf087037faf14b8bcf30533611531c31
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97326844"
---
# <a name="sysdm_os_memory_cache_clock_hands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o status de cada ponteiro de um relógio de cache específico.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_os_memory_cache_clock_hands**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Endereço do cache associado ao relógio. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Nome do cache. Não permite valor nulo.|  
|**tipo**|**nvarchar(60)**|Tipo de armazenamento de cache. Pode haver vários caches do mesmo tipo. Não permite valor nulo.|  
|**clock_hand**|**nvarchar(60)**|Tipo de mão. Ele é um dos seguintes:<br /><br /> Externo<br /><br /> Interna<br /><br /> Não permite valor nulo.|  
|**clock_status**|**nvarchar(60)**|Status do relógio. Ele é um dos seguintes:<br /><br /> Suspenso<br /><br /> Executando<br /><br /> Não permite valor nulo.|  
|**rounds_count**|**bigint**|Número de varreduras feitas no cache para remover entradas. Não permite valor nulo.|  
|**removed_all_rounds_count**|**bigint**|Número de entradas removidas por todas as varreduras. Não permite valor nulo.|  
|**updated_last_round_count**|**bigint**|Número de entradas atualizadas durante a última varredura. Não permite valor nulo.|  
|**removed_last_round_count**|**bigint**|Número de entradas removidas durante a última varredura. Não permite valor nulo.|  
|**last_tick_time**|**bigint**|Última hora, em milissegundos, que o ponteiro do relógio se moveu. Não permite valor nulo.|  
|**round_start_time**|**bigint**|Hora, em milissegundos, da varredura anterior. Não permite valor nulo.|  
|**last_round_start_time**|**bigint**|Tempo total, em milissegundos, que o relógio levou para concluir o giro anterior. Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena informações em memória em uma estrutura denominada cache de memória. As informações no cache podem ser dados, entradas de índice, planos de procedimento compilados e uma variedade de outros tipos de informações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar a recriação das informações, elas são retidas no cache de memória pelo maior prazo possível, sendo removidas normalmente do cache quando forem muito antigas para serem úteis ou quando o espaço de memória for necessário para novas informações. O processo que remove informações antigas é chamado de varredura de memória. A varredura de memória é uma atividade frequente, mas não é contínua. Um algoritmo de relógio controla a varredura do cache de memória. Cada relógio pode controlar várias varreduras de memória, que são chamadas de ponteiros. O ponteiro do relógio do cache de memória é o local atual de um dos ponteiros de uma varredura de memória.  

## <a name="see-also"></a>Consulte Também  
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [&#41;&#40;Transact-SQL de sys.dm_os_memory_cache_counters ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

