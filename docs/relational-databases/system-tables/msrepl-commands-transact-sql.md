---
description: MSrepl_commands (Transact-SQL)
title: MSrepl_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8596aefdaecce0e7d39033b2a484ebfe6a4f46b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540245"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSrepl_commands** contém linhas de comandos replicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|A ID do banco de dados Publicador.|  
|**xact_seqno**|**varbinary(16)**|O número de sequência da transação.|  
|**tipo**|**int**|O tipo de comando.|  
|**article_id**|**int**|A ID do artigo.|  
|**originator_id**|**int**|A ID do originador.|  
|**command_id**|**int**|A ID do comando.|  
|**partial_command**|**bit**|Indica se este é um comando parcial ou não.|  
|**command**|**varbinary (1024)**|O valor do comando.|  
|**hashkey**|**int**|Interno-somente uso.|  
|**originator_lsn**|**varbinary(16)**|Identifica o LSN para o comando na publicação de origem. Usado em replicação transacional ponto a ponto.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
