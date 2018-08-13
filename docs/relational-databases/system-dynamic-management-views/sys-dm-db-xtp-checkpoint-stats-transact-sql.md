---
title: sys.dm_db_xtp_checkpoint_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a8389ac173eb72c152eed3a7a8a40d8453dbed22
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39541446"
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas sobre as operações de ponto de verificação do OLTP na memória no banco de dados atual. Se o banco de dados não tiver nenhum objeto no OLTP na memória, retorna um conjunto de resultados vazio.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] é substancialmente diferente das versões mais recentes e é discutida quanto menor o tópico no [SQL Server 2014](#bkmk_2014).**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior  
 A tabela a seguir descreve as colunas na `sys.dm_db_xtp_checkpoint_stats`, começando com **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|Último LSN visto pelo controlador.|  
|end_of_log_lsn|**numeric(38)**|O LSN de final do log.|  
|bytes_to_end_of_log|**bigint**|Não processados por controlador, correspondentes aos bytes entre bytes de log `last_lsn_processed` e `end_of_log_lsn`.|  
|log_consumption_rate|**bigint**|Taxa de consumo de log de transações pelo controlador (em KB/s).|  
|active_scan_time_in_ms|**bigint**|Tempo gasto pelo controlador em verificar ativamente o log de transações.|  
|total_wait_time_in_ms|**bigint**|Tempo de espera cumulativa para o controlador ao não verificando o log.|  
|waits_for_io|**bigint**|Número de esperas do log de e/s incorrido pelo thread do controlador.|  
|io_wait_time_in_ms|**bigint**|Tempo acumulado gasto aguardando e/s de log pelo thread do controlador.|  
|waits_for_new_log_count|**bigint**|Número de esperas incorrido pelo thread do controlador para um novo log seja gerado.|  
|new_log_wait_time_in_ms|**bigint**|Tempo acumulado gasto aguardando em um novo log pelo thread do controlador.|  
|idle_attempts_count|**bigint**|Número de vezes que o controlador a transição para um estado ocioso.|  
|tx_segments_dispatched|**bigint**|Número de segmentos visto pelo controlador e enviado para os serializadores. Segmento é uma parte contígua de log que formam uma unidade de serialização. Ele é dimensionado no momento para 1MB, mas pode mudar no futuro.|  
|segment_bytes_dispatched|**bigint**|Contagem total de bytes de bytes expedidas pelo controlador para serializadores, uma vez que reiniciar o banco de dados.|  
|bytes_serialized|**bigint**|Contagem total de bytes serializados desde a reinicialização do banco de dados.|  
|serializer_user_time_in_ms|**bigint**|Tempo gasto pelos serializadores no modo de usuário.|  
|serializer_kernel_time_in_ms|**bigint**|Tempo gasto pelos serializadores no modo kernel.|  
|xtp_log_bytes_consumed|**bigint**|Contagem total de bytes de log consumidos desde a reinicialização do banco de dados.|  
|checkpoints_closed|**bigint**|Contagem de pontos de verificação fechados desde a reinicialização do banco de dados.|  
|last_closed_checkpoint_ts|**bigint**|Carimbo de hora do último ponto de verificação fechado.|  
|hardened_recovery_lsn|**numeric(38)**|Recuperação será iniciada a partir deste LSN.|  
|hardened_root_file_guid|**uniqueidentifier**|GUID do arquivo raiz que protegidos como resultado do último ponto de verificação concluído.|  
|hardened_root_file_watermark|**bigint**|**Interno apenas**. A distância é válido para ler o arquivo raiz até (esse é um tipo internamente relevante somente – chamado BSN).|  
|hardened_truncation_lsn|**numeric(38)**|LSN do ponto de truncamento.|  
|log_bytes_since_last_close|**bigint**|Bytes do último próximos ao final do log.|  
|time_since_last_close_in_ms|**bigint**|Tempo desde o último fechamento do ponto de verificação.|  
|current_checkpoint_id|**bigint**|Atualmente, novos segmentos estão sendo atribuídos a esse ponto de verificação. O sistema de ponto de verificação é um pipeline. O ponto de verificação atual é aquele que segmentos do log estão sendo atribuídos ao. Depois que ele atingiu o limite, o ponto de verificação é liberado, o controlador e um novo, criado como atual.|  
|current_checkpoint_segment_count|**bigint**|Contagem de segmentos no ponto de verificação atual.|  
|recovery_lsn_candidate|**bigint**|**Somente internamente**. Candidato a ser escolhido como recoverylsn quando current_checkpoint_id for fechado.|  
|outstanding_checkpoint_count|**bigint**|Número de pontos de verificação no pipeline aguardando para ser fechado.|  
|closing_checkpoint_id|**bigint**|ID do ponto de verificação de fechamento.<br /><br /> Os serializadores estiver trabalhando em paralelo, portanto, depois que eles terminaram o ponto de verificação é um candidato a ser encerrada pelo thread de fechamento. Mas o thread de fechamento só pode fechar um de cada vez e deve estar em ordem, para que o ponto de verificação do fechamento é aquele que está trabalhando para o thread de fechamento.|  
|recovery_checkpoint_id|**bigint**|ID do ponto de verificação a ser usado na recuperação.|  
|recovery_checkpoint_ts|**bigint**|Carimbo de hora do ponto de verificação de recuperação.|  
|bootstrap_recovery_lsn|**numeric(38)**|LSN de recuperação para o bootstrap.|  
|bootstrap_root_file_guid|**uniqueidentifier**|GUID do arquivo raiz para a inicialização.|  
|internal_error_code|**bigint**|Erro visto por qualquer do controlador, serializador, fechar e os threads de mesclagem.|
|bytes_of_large_data_serialized|**bigint**|A quantidade de dados que foi serializados. |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 A tabela a seguir descreve as colunas na `sys.dm_db_xtp_checkpoint_stats`, para **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|O número de bytes de log entre o LSN (número de sequência de log) atual do thread e o fim do log.|  
|total_log_blocks_processed|**bigint**|Número total de blocos de log processados desde a inicialização do servidor.|  
|total_log_records_processed|**bigint**|Número total de registros de log processados desde a inicialização do servidor.|  
|xtp_log_records_processed|**bigint**|Número total de registros de log processados do OLTP na memória desde a inicialização do servidor.|  
|total_wait_time_in_ms|**bigint**|Tempo de espera acumulado em ms.|  
|waits_for_io|**bigint**|Número de esperas da E/S do log.|  
|io_wait_time_in_ms|**bigint**|Tempo acumulado gasto aguardando E/S no log.|  
|waits_for_new_log|**bigint**|Número de esperas para que o novo log seja gerado.|  
|new_log_wait_time_in_ms|**bigint**|Tempo acumulado gasto aguardando novo log.|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|Quantidade de log gerado desde o último ponto de verificação do OLTP na memória.|  
|ms_since_last_checkpoint|**bigint**|Quantidade tempo em milissegundos desde o último ponto de verificação do OLTP na memória.|  
|checkpoint_lsn|**numeric (38)**|O LSN (número de sequência de log) de recuperação associado ao último ponto de verificação de OLTP na memória concluído.|  
|current_lsn|**numeric (38)**|O LSN do registro de log que está sendo processado.|  
|end_of_log_lsn|**numeric (38)**|O LSN do fim do log.|  
|task_address|**varbinary(8)**|O endereço da SOS_Task. Entre em sys.dm_os_tasks para localizar informações adicionais.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE` no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela otimizada em memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
