---
title: MSmerge_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4290f3d41cf4e5210a7fde98132db533f8336810
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903690"
---
# <a name="msmergesessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_sessions** tabela contém linhas de histórico com os resultados das sessões anteriores do trabalho do agente de mesclagem. Cada vez que o Merge Agent é executado, uma nova  linha é adicionada a essa tabela. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|A ID da sessão de trabalho do Merge Agent.|  
|**agent_id**|**int**|A ID do Merge Agent.|  
|**start_time**|**datetime**|A hora de início da execução do trabalho.|  
|**end_time**|**datetime**|A hora de término da execução do trabalho.|  
|**duration**|**int**|A duração acumulada, em segundos, dessa sessão de trabalho.|  
|**delivery_time**|**int**|O número de segundos necessário para aplicar um lote de alterações.|  
|**upload_time**|**int**|O número de segundos necessário para carregar alterações no Publicador.|  
|**download_time**|**int**|O número de segundos necessário para baixar alterações no Assinante.|  
|**delivery_rate**|**float**|O número médio de comandos fornecido por segundo.|  
|**time_remaining**|**int**|O número estimado de segundos que sobram em uma sessão ativa.|  
|**percent_complete**|**decimal**|A porcentagem estimada do total de alterações que já foi entregue em uma sessão ativa.|  
|**upload_inserts**|**int**|O número de inserções aplicadas ao Publicador.|  
|**upload_updates**|**int**|O número de atualizações aplicado ao Publicador.|  
|**upload_deletes**|**int**|O número de exclusões aplicadas no Publicador.|  
|**upload_conflicts**|**int**|O número de conflitos que ocorreu durante a aplicação de alterações no Publicador.|  
|**upload_conflicts_resolved**|**int**|O número de conflitos que ocorreu durante a aplicação de alterações no Publicador e que foi resolvido.|  
|**upload_rows_retried**|**int**|O número de linhas carregado no Publicador em nova tentativa.|  
|**download_inserts**|**int**|O número de inserções aplicado ao Assinante.|  
|**download_updates**|**int**|O número de atualizações aplicado ao Assinante.|  
|**download_deletes**|**int**|O número de exclusões aplicadas no Assinante.|  
|**download_conflicts**|**int**|O número de conflitos que ocorreu durante a aplicação de alterações no Assinante.|  
|**download_conflicts_resolved**|**int**|O número de conflitos que ocorreu durante a aplicação de alterações no Assinante e que foi resolvido.|  
|**download_rows_retried**|**int**|O número de linhas baixado no Assinante em nova tentativa.|  
|**schema_changes**|**int**|O número de alterações de esquema aplicado durante a sessão.|  
|**metadata_rows_cleanedup**|**int**|O número de linhas de metadados limpos durante a sessão.|  
|**runstatus**|**int**|O status da execução:<br /><br /> **1** = Start.<br /><br /> **2** = êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = Fail.|  
|**estimated_upload_changes**|**int**|O número estimado de alterações que precisa ser aplicado ao Publicador.|  
|**estimated_download_changes**|**int**|O número estimado de alterações que precisa ser aplicado ao Assinante.|  
|**connection_type**|**int**|A conexão usada durante o carregamento:<br /><br /> **1** = rede local (LAN).<br /><br /> **2** = conexão de rede dial-up.<br /><br /> **3** = sincronização da web.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
