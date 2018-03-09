---
title: MSreplication_queue (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25bbbc37215010d60cd20a01ea06cb35176eabf5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_queue** tabela é usada pelo processo de replicação para armazenar comandos enfileirados emitidos por todas as assinaturas de atualização na fila que estão usando com base em SQL na fila. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Publicador**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**tranid**|**sysname**|A ID da transação na qual o comando enfileirado foi executado.|  
|**dados**|**varbinary (8000)**|O pacote de fluxo de bytes que armazenou informações sobre os comandos na fila.|  
|**datalen**|**int**|O comprimento dos dados, em bytes.|  
|**CommandType**|**int**|O tipo de comando que está sendo enfileirado:<br /><br /> 1 = Comando de usuário na transação.<br /><br /> 2 = Comando de sincronização de assinatura.|  
|**insertdate**|**datetime**|A data da inserção.|  
|**orderkey**|**bigint**|A coluna de identidade que aumenta de forma monotônica.|  
|**cmdstate**|**bit**|O estado do comando:<br /><br /> 0 = Completo.<br /><br /> 1 = Parcial.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
