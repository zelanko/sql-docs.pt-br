---
title: MSrepl_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70d737e8c73d3e5b6876c2669fbafbc71bea66e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986473"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSrepl_errors** contém linhas com agente de distribuição estendido e informações de agente de mesclagem falha. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|A ID do erro.|  
|**time**|**datetime**|A hora da ocorrência do erro.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|A ID de tipo de origem do erro.|  
|**source_name**|**nvarchar (100)**|O nome de origem do erro.|  
|**error_code**|**sysname**|O código do erro.|  
|**error_text**|**ntext**|A mensagem de erro.|  
|**xact_seqno**|**varbinary (16)**|O número de sequência do log de transações inicial do lote de execução com falha. Usado somente por Distribution Agents, esse é o número de sequência do log de transações da primeira transação do lote de execução com falha.|  
|**command_id**|**int**|A ID de comando do lote de execução com falha. Usado somente por Distribution Agents, essa é a ID de comando do primeiro comando do lote de execução com falha.|  
|**session_id**|**int**|A ID da sessão de agente na qual ocorreu o erro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
