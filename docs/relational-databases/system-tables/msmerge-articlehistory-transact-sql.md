---
title: MSmerge_articlehistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 256a2c3ca6801e09bed0a96a63cc6d6540d466ff
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791508"
---
# <a name="msmergearticlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_articlehistory** tabela rastreia as alterações feitas aos artigos durante uma sessão de sincronização do agente de mesclagem, com uma linha para cada artigo no qual foram feitas alterações. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|A ID de uma sessão de trabalho do agente de mesclagem na [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) tabela do sistema.|  
|**phase_id**|**int**|A fase da sessão de sincronização, que pode ser uma das seguintes:<br /><br /> **1** = carregamento.<br /><br /> **2** = download.<br /><br /> **4** = limpeza.<br /><br /> **5** = desligamento.<br /><br /> **6** = as alterações de esquema.<br /><br /> **7** = BCP.|  
|**article_name**|**sysname**|O nome do artigo no qual as alterações foram feitas.|  
|**start_time**|**datetime**|A hora em que o agente começou a processar o artigo.|  
|**duration**|**int**|O período de tempo em que o agente processou um artigo, em segundos.|  
|**Insere**|**int**|O número de inserções aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**atualizações**|**int**|O número de atualizações aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**exclusões**|**int**|O número de exclusões aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**conflitos**|**int**|O número de conflitos que ocorreu durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**conflicts_resolved**|**int**|O número de conflitos que ocorreu e foi resolvido durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**rows_retried**|**int**|O número de linhas com falha recuperado durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**percent_complete**|**decimal**|A porcentagem do tempo total de sincronização que Merge Agent gastou no artigo durante uma sessão. Esse valor será NULL até que a sessão seja concluída.|  
|**estimated_changes**|**int**|Uma estimativa de alterações do número de linhas que deve ser se aplicado ao artigo.|  
|**relative_cost**|**decimal**|O tempo gasto na aplicação de alterações a este artigo comparado com o tempo total de toda a sessão|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
