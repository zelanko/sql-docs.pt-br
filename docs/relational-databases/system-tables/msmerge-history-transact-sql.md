---
description: MSmerge_history (Transact-SQL)
title: MSmerge_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 348df963920d35aeb874a83cad83701995d563cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540859"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_history** contém linhas de histórico com descrições detalhadas dos resultados das sessões de trabalho agente de mesclagem anteriores. Essa tabela contém uma linha para cada linha de saída de agente. Essa tabela é usada no banco de dados de distribuição e em cada banco de dados de assinatura. No banco de dados de distribuição, contém histórico de todas as publicações de mesclagem e assinatura que usam o Distribuidor. Em cada banco de dados de assinatura, contém o histórico de publicações que o Assinante assina.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|A ID de trabalho do Merge Agent.|  
|**agent_id**|**int**|A ID do Merge Agent.|  
|**feitos**|**nvarchar(255)**|O texto de mensagem.|  
|**error_id**|**int**|A ID de um erro na tabela do sistema [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) .|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
|**updatable_row**|**bit**|Defina como **1** se a linha do histórico puder ser substituída.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
