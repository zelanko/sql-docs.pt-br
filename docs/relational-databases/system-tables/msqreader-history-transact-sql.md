---
title: MSqreader_history (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c9615bb702c89d8b2a5be0087671df9d8a6a910
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msqreaderhistory-transact-sql"></a>MSqreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSqreader_history** tabela contém linhas de histórico para o Queue Reader Agents associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Queue Reader Agent.|  
|**publication_id**|**int**|A ID da publicação.|  
|**runstatus**|**int**|O estado de execução do agente:<br /><br /> **1** = iniciar.<br /><br /> **2** = êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A data e hora de início da sessão do agente.|  
|**time**|**datetime**|A data e a hora da última mensagem registrada.|  
|**duration**|**int**|O tempo decorrido da atividade de sessão registrada, em segundos.|  
|**comentários**|**nvarchar(255)**|O texto descritivo.|  
|**transaction_id**|**nvarchar (40)**|A ID da transação armazenada com a mensagem, se aplicável.|  
|**transaction_status**|**int**|O status da transação.|  
|**transactions_processed**|**int**|O número acumulado de transações processadas na sessão.|  
|**commands_processed**|**int**|O número acumulado de comandos processados na sessão.|  
|**delivery_rate**|**float(53)**|O número médio de comandos entregues por segundo.|  
|**transaction_rate**|**float(53)**|A taxa de transações processadas.|  
|**Assinante**|**sysname**|O nome do Assinante.|  
|**subscriberdb**|**sysname**|O nome do banco de dados de assinatura.|  
|**error_id**|**int**|Caso não seja zero, o número representa um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de erro.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora para a tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
