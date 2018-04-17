---
title: os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79d6ca163f2df910825e7000372b70cb6814b839
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosthreads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma lista de todos os threads do Sistema Operacional [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executados sob o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_threads**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|Endereço de memória (Chave Primária) do thread.|  
|started_by_sqlservr|**bit**|Indica o iniciador de thread.<br /><br /> 1 = O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciou o thread.<br /><br /> 0 = Outro componente iniciou o thread, como um procedimento armazenado estendido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**Int**|ID do thread atribuído pelo sistema operacional.|  
|status|**Int**|Sinalizador de estado interno.|  
|instruction_address|**varbinary(8)**|Endereço da instrução que está sendo executada atualmente.|  
|creation_time|**datetime**|Hora em que esse thread foi criado.|  
|kernel_time|**bigint**|Tempo de kernel usado por esse thread.|  
|usermode_time|**bigint**|Tempo do usuário usado por esse thread.|  
|stack_base_address|**varbinary(8)**|Endereço de memória do endereço de pilha mais alto para esse thread.|  
|stack_end_address|**varbinary(8)**|Endereço de memória do endereço de pilha mais baixo desse thread.|  
|stack_bytes_committed|**Int**|Número de bytes confirmados na pilha.|  
|stack_bytes_used|**Int**|Número de bytes ativamente usados no thread.|  
|affinity|**bigint**|Máscara de CPU na qual este thread está sendo executado. Isso depende do valor configurado pelo **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY** instrução. Pode ser diferente do agendador em caso de afinidade flexível.|  
|Prioridade|**Int**|Valor de prioridade deste thread.|  
|Localidade|**Int**|LCID de localidade em cache do thread.|  
|Token|**varbinary(8)**|Identificador de token de representação em cache para o thread.|  
|is_impersonating|**Int**|Indica se esse thread está usando a representação do Win32.<br /><br /> 1 = O thread está usando credenciais de segurança que são diferentes do padrão do processo. Isso indica que o thread está representando uma entidade diferente daquela que criou o processo.|  
|is_waiting_on_loader_lock|**Int**|Status do sistema operacional indicando se o thread está aguardando o bloqueio de carregador.|  
|fiber_data|**varbinary(8)**|Fibra do Win32 atual sendo executada no thread. Só é aplicável quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para lightweight pooling.|  
|thread_handle|**varbinary(8)**|Somente para uso interno.|  
|event_handle|**varbinary(8)**|Somente para uso interno.|  
|scheduler_address|**varbinary(8)**|Endereço de memória do agendador associado a esse thread. Para obter mais informações, consulte [sys.DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary(8)**|Endereço de memória do trabalhador ligado a esse thread. Para obter mais informações, consulte [sys.DM os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary(8)**|Endereço de contexto de fibra interno. Só é aplicável quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para lightweight pooling.|  
|self_address|**varbinary(8)**|Ponteiro de consistência interno.|  
|processor_group|**smallint**|**Aplica-se a**: do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do grupo de processadores.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="examples"></a>Exemplos  
 Na inicialização, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia threads e associa os trabalhadores a esses threads. Porém, componentes externos, como um procedimento armazenado estendido, podem iniciar threads sob o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem nenhum controle desses threads. os_threads pode fornecer informações sobre threads não autorizados que consomem recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo.  
  
 A consulta a seguir é usada para localizar trabalhadores, e o tempo usado para execução, que estejam executando threads não iniciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Visando a concisão, a consulta a seguir usa um asterisco (`*`) na instrução `SELECT`. Deve-se evitar o uso do asterisco (*), especialmente em exibições do catálogo, exibições de administração dinâmicas e funções com valor de tabela do sistema. Futuras atualizações e versões de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode adicionar colunas e alterar a ordem das colunas nessas exibições e funções. Essas mudanças poderão interromper aplicativos que esperam uma ordem e um número de colunas específicos.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Consulte também  
  [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


