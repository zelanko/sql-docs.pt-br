---
title: sys. dm_db_xtp_checkpoint_stats (Transact-SQL) | Microsoft Docs
description: Retorna estatísticas sobre as operações de ponto de verificação do OLTP na memória no banco de dados atual. Saiba como essa exibição difere em versões do SQL Server.
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
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
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66532a6ed19dc3a7929fe7d5638fa850c893d119
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542279"
---
# <a name="sysdm_db_xtp_checkpoint_stats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Retorna estatísticas sobre as operações de ponto de verificação do OLTP na memória no banco de dados atual. Se o banco de dados não tiver nenhum objeto no OLTP na memória, retorna um conjunto de resultados vazio.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
```  
USE In_Memory_db_name
SELECT * FROM sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] é substancialmente diferente das versões mais recentes e é discutido no tópico em [SQL Server 2014](#bkmk_2014).**
  
## <a name="sssql15-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior  
 A tabela a seguir descreve as colunas no `sys.dm_db_xtp_checkpoint_stats` , começando com **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** .  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|Último LSN visto pelo controlador.|  
|end_of_log_lsn|**numeric (38)**|O LSN do final do log.|  
|bytes_to_end_of_log|**bigint**|Bytes de log não processados pelo controlador, correspondentes aos bytes entre `last_lsn_processed` e `end_of_log_lsn` .|  
|log_consumption_rate|**bigint**|Taxa de consumo de log de transações pelo controlador (em KB/s).|  
|active_scan_time_in_ms|**bigint**|Tempo gasto pelo controlador no exame ativo do log de transações.|  
|total_wait_time_in_ms|**bigint**|Tempo de espera cumulativo para o controlador ao não verificar o log.|  
|waits_for_io|**bigint**|Número de esperas para a e/s de log incorridas pelo thread do controlador.|  
|io_wait_time_in_ms|**bigint**|Tempo cumulativo gasto aguardando e/s de log pelo thread do controlador.|  
|waits_for_new_log_count|**bigint**|Número de esperas cobradas pelo thread do controlador para que um novo log seja gerado.|  
|new_log_wait_time_in_ms|**bigint**|Tempo cumulativo gasto aguardando um novo log pelo thread do controlador.|  
|idle_attempts_count|**bigint**|Número de vezes que o controlador passou para um estado ocioso.|  
|tx_segments_dispatched|**bigint**|Número de segmentos vistos pelo controlador e expedidos para os serializadores. Segment é uma parte contígua do log que forma uma unidade de serialização. Ele está atualmente dimensionado para 1MB, mas pode ser alterado no futuro.|  
|segment_bytes_dispatched|**bigint**|Contagem total em bytes de bytes expedidos pelo controlador para serializadores, desde a reinicialização do banco de dados.|  
|bytes_serialized|**bigint**|Contagem total de bytes serializados desde a reinicialização do banco de dados.|  
|serializer_user_time_in_ms|**bigint**|Tempo gasto pelos serializadores no modo de usuário.|  
|serializer_kernel_time_in_ms|**bigint**|Tempo gasto pelos serializadores no modo kernel.|  
|xtp_log_bytes_consumed|**bigint**|Contagem total de bytes de log consumidos desde a reinicialização do banco de dados.|  
|checkpoints_closed|**bigint**|Contagem de pontos de verificação fechados desde a reinicialização do banco de dados.|  
|last_closed_checkpoint_ts|**bigint**|Carimbo de data/hora do último ponto de verificação fechado.|  
|hardened_recovery_lsn|**numeric (38)**|A recuperação será iniciada a partir desse LSN.|  
|hardened_root_file_guid|**uniqueidentifier**|GUID do arquivo raiz que foi protegido como resultado do último ponto de verificação concluído.|  
|hardened_root_file_watermark|**bigint**|**Somente interno**. Até onde é válido ler o arquivo raiz até (esse é um tipo interno relevante apenas, chamado BSN).|  
|hardened_truncation_lsn|**numeric (38)**|LSN do ponto de truncamento.|  
|log_bytes_since_last_close|**bigint**|Bytes do último próximo ao fim do log atual.|  
|time_since_last_close_in_ms|**bigint**|Tempo desde o último fechamento do ponto de verificação.|  
|current_checkpoint_id|**bigint**|Atualmente, novos segmentos estão sendo atribuídos a este ponto de verificação. O sistema de ponto de verificação é um pipeline. O ponto de verificação atual é aquele ao qual os segmentos do log estão sendo atribuídos. Depois de atingir um limite, o ponto de verificação é liberado pelo controlador e um novo é criado como atual.|  
|current_checkpoint_segment_count|**bigint**|Contagem de segmentos no ponto de verificação atual.|  
|recovery_lsn_candidate|**bigint**|**Somente internamente**. Candidato a ser escolhido como recoverylsn quando current_checkpoint_id for fechado.|  
|outstanding_checkpoint_count|**bigint**|Número de pontos de verificação no pipeline aguardando para serem fechados.|  
|closing_checkpoint_id|**bigint**|ID do ponto de verificação de fechamento.<br /><br /> Os serializadores estão trabalhando em paralelo, portanto, depois que eles forem concluídos, o ponto de verificação será um candidato a ser fechado pelo thread fechado. Mas o thread de fechamento só pode fechar um de cada vez e deve estar em ordem, portanto, o ponto de verificação de fechamento é aquele em que o thread de fechamento está trabalhando.|  
|recovery_checkpoint_id|**bigint**|ID do ponto de verificação a ser usado na recuperação.|  
|recovery_checkpoint_ts|**bigint**|Carimbo de data/hora do ponto de verificação de recuperação.|  
|bootstrap_recovery_lsn|**numeric (38)**|LSN de recuperação para a inicialização.|  
|bootstrap_root_file_guid|**uniqueidentifier**|GUID do arquivo raiz para a inicialização.|  
|internal_error_code|**bigint**|Erro visto por qualquer um dos threads de controlador, serializador, fechamento e mesclagem.|
|bytes_of_large_data_serialized|**bigint**|A quantidade de dados serializados. |  
  
##  <a name="sssql14"></a><a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 A tabela a seguir descreve as colunas no `sys.dm_db_xtp_checkpoint_stats` , para **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** .  
  
|Nome da coluna|Type|Descrição|  
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
|task_address|**varbinary (8)**|O endereço da SOS_Task. Entre em sys.dm_os_tasks para localizar informações adicionais.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE` no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
