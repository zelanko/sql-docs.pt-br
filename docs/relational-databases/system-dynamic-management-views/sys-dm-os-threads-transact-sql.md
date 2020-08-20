---
description: sys.dm_os_threads (Transact-SQL)
title: sys. dm_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80986f9bce91034d8950915f5048e3f4ee895f57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474818"
---
# <a name="sysdm_os_threads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma lista de todos os threads do Sistema Operacional [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executados sob o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_threads**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary (8)**|Endereço de memória (Chave Primária) do thread.|  
|started_by_sqlservr|**bit**|Indica o iniciador de thread.<br /><br /> 1 = O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciou o thread.<br /><br /> 0 = Outro componente iniciou o thread, como um procedimento armazenado estendido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**int**|ID do thread atribuído pelo sistema operacional.|  
|status|**int**|Sinalizador de estado interno.|  
|instruction_address|**varbinary (8)**|Endereço da instrução que está sendo executada atualmente.|  
|creation_time|**datetime**|Hora em que esse thread foi criado.|  
|kernel_time|**bigint**|Tempo de kernel usado por esse thread.|  
|usermode_time|**bigint**|Tempo do usuário usado por esse thread.|  
|stack_base_address|**varbinary (8)**|Endereço de memória do endereço de pilha mais alto para esse thread.|  
|stack_end_address|**varbinary (8)**|Endereço de memória do endereço de pilha mais baixo desse thread.|  
|stack_bytes_committed|**int**|Número de bytes confirmados na pilha.|  
|stack_bytes_used|**int**|Número de bytes ativamente usados no thread.|  
|affinity|**bigint**|Máscara de CPU na qual este thread está sendo executado. Isso depende do valor configurado pela instrução **ALTER Server Configuration Set Process Affinity** Statement. Pode ser diferente do agendador em caso de afinidade flexível.|  
|Prioridade|**int**|Valor de prioridade deste thread.|  
|Local|**int**|LCID de localidade em cache do thread.|  
|Token|**varbinary (8)**|Identificador de token de representação em cache para o thread.|  
|is_impersonating|**int**|Indica se esse thread está usando a representação do Win32.<br /><br /> 1 = O thread está usando credenciais de segurança que são diferentes do padrão do processo. Isso indica que o thread está representando uma entidade diferente daquela que criou o processo.|  
|is_waiting_on_loader_lock|**int**|Status do sistema operacional indicando se o thread está aguardando o bloqueio de carregador.|  
|fiber_data|**varbinary (8)**|Fibra do Win32 atual sendo executada no thread. Só é aplicável quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para lightweight pooling.|  
|thread_handle|**varbinary (8)**|Somente para uso interno.|  
|event_handle|**varbinary (8)**|Somente para uso interno.|  
|scheduler_address|**varbinary (8)**|Endereço de memória do agendador associado a esse thread. Para obter mais informações, consulte [Sys. dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary (8)**|Endereço de memória do trabalhador ligado a esse thread. Para obter mais informações, consulte [Sys. dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary (8)**|Endereço de contexto de fibra interno. Só é aplicável quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para lightweight pooling.|  
|self_address|**varbinary (8)**|Ponteiro de consistência interno.|  
|processor_group|**smallint**|**Aplica-se a**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e posterior.<br /><br /> ID do grupo de processadores.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="notes-on-linux-version"></a>Observações sobre a versão do Linux

Devido a como o mecanismo do SQL funciona no Linux, algumas dessas informações não correspondem aos dados de diagnóstico do Linux. Por exemplo, não `os_thread_id` corresponde ao resultado de ferramentas como `ps` , `top` ou procfs (/proc/ `pid` ).  Isso ocorre devido à SQLPAL (camada de abstração de plataforma), uma camada entre SQL Server componentes e o sistema operacional.

## <a name="examples"></a>Exemplos  
 Na inicialização, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia threads e associa os trabalhadores a esses threads. Porém, componentes externos, como um procedimento armazenado estendido, podem iniciar threads sob o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem nenhum controle desses threads. o sys. dm_os_threads pode fornecer informações sobre threads não autorizados que consomem recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo.  
  
 A consulta a seguir é usada para localizar trabalhadores, e o tempo usado para execução, que estejam executando threads não iniciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]
>  Visando a concisão, a consulta a seguir usa um asterisco (`*`) na instrução `SELECT`. Deve-se evitar o uso do asterisco (*), especialmente em exibições do catálogo, exibições de administração dinâmicas e funções com valor de tabela do sistema. Atualizações e versões futuras do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem adicionar colunas e alterar a ordem das colunas para essas exibições e funções. Essas mudanças poderão interromper aplicativos que esperam uma ordem e um número de colunas específicos.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Consulte Também  
  [sys. dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


