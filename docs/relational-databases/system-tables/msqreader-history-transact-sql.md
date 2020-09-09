---
description: MSqreader_history (Transact-SQL)
title: MSqreader_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 65f1330aa14e52b3295a9514060ca9244721028b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540258"
---
# <a name="msqreader_history-transact-sql"></a>MSqreader_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSqreader_history** contém linhas de histórico para os agentes de leitor de fila associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Queue Reader Agent.|  
|**publication_id**|**int**|A ID da publicação.|  
|**runstatus**|**int**|O estado de execução do agente:<br /><br /> **1** = iniciar.<br /><br /> **2** = com sucesso.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = tentar novamente.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A data e hora de início da sessão do agente.|  
|**time**|**datetime**|A data e a hora da última mensagem registrada.|  
|**duration**|**int**|O tempo decorrido da atividade de sessão registrada, em segundos.|  
|**feitos**|**nvarchar(255)**|O texto descritivo.|  
|**transaction_id**|**nvarchar(40)**|A ID da transação armazenada com a mensagem, se aplicável.|  
|**transaction_status**|**int**|O status da transação.|  
|**transactions_processed**|**int**|O número acumulado de transações processadas na sessão.|  
|**commands_processed**|**int**|O número acumulado de comandos processados na sessão.|  
|**delivery_rate**|**float(53)**|O número médio de comandos entregues por segundo.|  
|**transaction_rate**|**float(53)**|A taxa de transações processadas.|  
|**farão**|**sysname**|O nome do Assinante.|  
|**SubscriberDB**|**sysname**|O nome do banco de dados de assinatura.|  
|**error_id**|**int**|Se não for zero, o número representará uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de erro.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora para a tabela.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
