---
title: MSqreader_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c060cd85f1b4a36087f3d8756bf0d48c1976110f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msqreaderhistory-transact-sql"></a>MSqreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSqreader_history** tabela contém linhas de histórico para o Queue Reader Agents associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**Int**|A ID do Queue Reader Agent.|  
|**publication_id**|**Int**|A ID da publicação.|  
|**runstatus**|**Int**|O estado de execução do agente:<br /><br /> **1** = iniciar.<br /><br /> **2** = êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A data e hora de início da sessão do agente.|  
|**time**|**datetime**|A data e a hora da última mensagem registrada.|  
|**duration**|**Int**|O tempo decorrido da atividade de sessão registrada, em segundos.|  
|**Comentários**|**nvarchar(255)**|O texto descritivo.|  
|**transaction_id**|**nvarchar(40)**|A ID da transação armazenada com a mensagem, se aplicável.|  
|**transaction_status**|**Int**|O status da transação.|  
|**transactions_processed**|**Int**|O número acumulado de transações processadas na sessão.|  
|**commands_processed**|**Int**|O número acumulado de comandos processados na sessão.|  
|**delivery_rate**|**float(53)**|O número médio de comandos entregues por segundo.|  
|**transaction_rate**|**float(53)**|A taxa de transações processadas.|  
|**Assinante**|**sysname**|O nome do Assinante.|  
|**subscriberdb**|**sysname**|O nome do banco de dados de assinatura.|  
|**error_id**|**Int**|Caso não seja zero, o número representa um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de erro.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora para a tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
