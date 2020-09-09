---
description: MSmerge_articlehistory (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5fcf637d540b541f0a96e6a8f8322c34799ddcb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544511"
---
# <a name="msmerge_articlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_articlehistory** controla as alterações feitas nos artigos durante uma sessão de sincronização agente de mesclagem, com uma linha para cada artigo para o qual as alterações foram feitas. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|A ID de uma sessão de trabalho Agente de Mesclagem na tabela do sistema [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) .|  
|**phase_id**|**int**|A fase da sessão de sincronização, que pode ser uma das seguintes:<br /><br /> **1** = carregar.<br /><br /> **2** = baixar.<br /><br /> **4** = limpar.<br /><br /> **5** = desligar.<br /><br /> **6** = alterações de esquema.<br /><br /> **7** = bcp.|  
|**article_name**|**sysname**|O nome do artigo no qual as alterações foram feitas.|  
|**start_time**|**datetime**|A hora em que o agente começou a processar o artigo.|  
|**duration**|**int**|O período de tempo em que o agente processou um artigo, em segundos.|  
|**suplementos**|**int**|O número de inserções aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**atualizações**|**int**|O número de atualizações aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**excluído**|**int**|O número de exclusões aplicadas a um artigo específico durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**entrar**|**int**|O número de conflitos que ocorreu durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**conflicts_resolved**|**int**|O número de conflitos que ocorreu e foi resolvido durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**rows_retried**|**int**|O número de linhas com falha recuperado durante a sincronização. Esse valor será incrementado durante o processo de sincronização e o valor final representa o número total.|  
|**percent_complete**|**decimal**|A porcentagem do tempo total de sincronização que Merge Agent gastou no artigo durante uma sessão. Esse valor será NULL até que a sessão seja concluída.|  
|**estimated_changes**|**int**|Uma estimativa de alterações do número de linhas que deve ser se aplicado ao artigo.|  
|**relative_cost**|**decimal**|O tempo gasto na aplicação de alterações a este artigo comparado com o tempo total de toda a sessão|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
