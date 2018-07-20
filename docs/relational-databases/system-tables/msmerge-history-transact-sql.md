---
title: MSmerge_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a46c6c1ebaad6cb24ce8ad6bd3185cda74768113
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103624"
---
# <a name="msmergehistory-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_history** tabela contém linhas de histórico com descrições detalhadas dos resultados de sessões anteriores do trabalho do agente de mesclagem. Essa tabela contém uma linha para cada linha de saída de agente. Essa tabela é usada no banco de dados de distribuição e em cada banco de dados de assinatura. No banco de dados de distribuição, contém histórico de todas as publicações de mesclagem e assinatura que usam o Distribuidor. Em cada banco de dados de assinatura, contém o histórico de publicações que o Assinante assina.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|A ID de trabalho do Merge Agent.|  
|**agent_id**|**int**|A ID do Merge Agent.|  
|**Comentários**|**nvarchar(255)**|O texto da mensagem.|  
|**error_id**|**int**|A ID de um erro na [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) tabela do sistema.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
|**updatable_row**|**bit**|Definido como **1** se a linha de histórico pode ser substituída.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
