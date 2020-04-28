---
title: sys. dm_repl_traninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_traninfo
- dm_repl_traninfo
- sys.dm_repl_traninfo_TSQL
- dm_repl_traninfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_traninfo dynamic management view
ms.assetid: 5abe2605-0506-46ec-82b5-6ec08428ba13
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc4f107ef1c26aa51f3f1d58f910be9721f2a51a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68067829"
---
# <a name="sysdm_repl_traninfo-transact-sql"></a>sys.dm_repl_traninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre cada transação replicada ou do Change Data Capture.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**fp2p_pub_exists**|**tinyint**|Se a transação estiver em um banco de dados publicado com o uso de replicação transacional ponto a ponto. Se verdadeiro, o valor será 1; caso contrário, será 0.|  
|**db_ver**|**int**|Versão do banco de dados.|  
|**comp_range_address**|**varbinary (8)**|Define um intervalo de reversão parcial que deve ser ignorado.|  
|**textinfo_address**|**varbinary (8)**|Endereço na memória da estrutura de informações do texto em cache.|  
|**fsinfo_address**|**varbinary (8)**|Endereço na memória da estrutura de informações do fluxo de arquivos em cache.|  
|**begin_lsn**|**nvarchar (64)**|Número de sequência de log (LSN) do registro de log inicial da transação.|  
|**commit_lsn**|**nvarchar (64)**|LSN de registro de log de confirmação da transação.|  
|**DBID**|**smallint**|ID do banco de dados.|  
|**as**|**int**|ID do comando replicado na transação.|  
|**xdesid**|**nvarchar (64)**|ID da transação.|  
|**artcache_table_address**|**varbinary (8)**|Endereço na memória da estrutura de tabela de artigo em cache usada pela última vez nesta transação.|  
|**servidor**|**nvarchar (514)**|Nome de servidor.|  
|**server_len_in_bytes**|**smallint**|Comprimento de caracteres, em bytes, do nome do servidor.|  
|**database**|**nvarchar (514)**|nome do banco de dados.|  
|**db_len_in_bytes**|**smallint**|Comprimento de caracteres, em bytes, do nome do banco de dados.|  
|**autor**|**nvarchar (514)**|Nome do servidor em que a transação foi originada.|  
|**originator_len_in_bytes**|**smallint**|Comprimento de caracteres, em bytes, do servidor em que a transação foi originada.|  
|**orig_db**|**nvarchar (514)**|Nome do banco de dados em que a transação foi originada.|  
|**orig_db_len_in_bytes**|**smallint**|Comprimento de caracteres, em bytes, do banco de dados em que a transação foi originada.|  
|**cmds_in_tran**|**int**|Número de comandos replicados na transação atual, que é usado para determinar quando uma transação lógica deve ser confirmada.|  
|**is_boundedupdate_singleton**|**tinyint**|Especifica se uma atualização de coluna exclusiva afeta apenas uma linha.|  
|**begin_update_lsn**|**nvarchar (64)**|LSN usado em uma atualização de coluna exclusiva.|  
|**delete_lsn**|**nvarchar (64)**|LSN a excluir como parte de uma atualização.|  
|**last_end_lsn**|**nvarchar (64)**|Último LSN em uma transação lógica.|  
|**fcomplete**|**tinyint**|Especifica se o comando é uma atualização parcial.|  
|**fcompensated**|**tinyint**|Especifica se a transação está envolvida em uma reversão parcial.|  
|**fprocessingtext**|**tinyint**|Especifica se a transação inclui uma coluna de tipo de dados grandes binários.|  
|**max_cmds_in_tran**|**int**|Número máximo de comandos em uma transação lógica, como especificado pelo Log Reader Agent.|  
|**begin_time**|**datetime**|Hora em que a transação foi iniciada.|  
|**commit_time**|**datetime**|Hora em que a transação foi confirmada.|  
|**session_id**|**int**|ID da sessão de verificação do log do Change Data Capture. Essa coluna é mapeada para a coluna **session_id** em [Sys. dm_cdc_logscan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**session_phase**|**int**|Número que indica a fase em que a sessão estava na ocasião em que o erro ocorreu. Essa coluna é mapeada para a coluna **phase_number** em [Sys. dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md).|  
|**is_known_cdc_tran**|**bit**|Indica a transação controlada pelo Change Data Capture.<br /><br /> 0 = Transação de replicação de transações.<br /><br /> 1 = Transação do Change Data Capture.|  
|**error_count**|**int**|Número de erros encontrados.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados de publicação ou no banco de dados habilitado para Change Data Capture.  
  
## <a name="remarks"></a>Comentários  
 As informações só serão retornadas para objetos de banco de dados replicados ou tabelas habilitadas para Change Data Capture atualmente armazenados no cache de artigo.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à replicação &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)   
 [Exibições de gerenciamento dinâmico relacionadas à captura de dados de alterações &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)  
  
  

