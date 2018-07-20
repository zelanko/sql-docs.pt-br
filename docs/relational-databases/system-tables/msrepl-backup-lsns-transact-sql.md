---
title: MSrepl_backup_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2978827ac47e46e7d9a5af7770101be52981b41f
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101434"
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSrepl_backup_lsns** tabela contém os números de sequência de log de transação (LSN) para oferecer suporte a opção 'Sincronizar com backup' do banco de dados de distribuição. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|A ID do banco de dados Publicador.|  
|**valid_xact_id**|**varbinary(16)**|A ID da transação a ser enviada ao Publicador para marcar o ponto de truncamento do log. Usado somente se o banco de dados de distribuição está no modo 'Sincronizar com backup'. Contém a ID da última transação replicada no banco de dados de Distribuição do qual foi feito backup. Será enviado ao Publicador para marcar o ponto de truncamento do log pelo Log Reader.|  
|**valid_xact_seqno**|**varbinary(16)**|O número de sequência da transação a ser enviada ao Publicador para marcar o ponto de truncamento do log. Usado somente se o banco de dados de Distribuição estiver no modo 'sincronizar com backup'. O número de sequência do log da última transação replicada no banco de dados de Distribuição do qual foi feito backup. Será enviado ao Publicador para marcar o ponto de truncamento do log pelo Log Reader.|  
|**next_xact_id**|**varbinary(16)**|O número de sequência de log temporário usado por operações de backup.|  
|**nextx_xact_seqno**|**varbinary(16)**|O número de sequência de log temporário usado por operações de backup.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
