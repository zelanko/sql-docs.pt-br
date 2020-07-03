---
title: MSrepl_backup_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c1870e9fba39995f7f8634076c658d8ef044999
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889533"
---
# <a name="msrepl_backup_lsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSrepl_backup_lsns** contém os números de sequência de log de transações (LSN) para dar suporte à opção ' sincronizar com backup ' do banco de dados de distribuição. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|A ID do banco de dados Publicador.|  
|**valid_xact_id**|**varbinary(16)**|A ID da transação a ser enviada ao Publicador para marcar o ponto de truncamento do log. Usado somente se o banco de dados de distribuição estiver no modo ' sincronizar com o backup '. Contém a ID da última transação replicada no banco de dados de Distribuição do qual foi feito backup. Será enviado ao Publicador para marcar o ponto de truncamento do log pelo Log Reader.|  
|**valid_xact_seqno**|**varbinary(16)**|O número de sequência da transação a ser enviada ao Publicador para marcar o ponto de truncamento do log. Usado somente se o banco de dados de Distribuição estiver no modo 'sincronizar com backup'. O número de sequência do log da última transação replicada no banco de dados de Distribuição do qual foi feito backup. Será enviado ao Publicador para marcar o ponto de truncamento do log pelo Log Reader.|  
|**next_xact_id**|**varbinary(16)**|O número de sequência de log temporário usado por operações de backup.|  
|**nextx_xact_seqno**|**varbinary(16)**|O número de sequência de log temporário usado por operações de backup.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
