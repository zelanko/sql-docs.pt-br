---
description: MSdistributiondbs (Transact-SQL)
title: MSdistributiondbs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 70140091cdd3027538038301a86bc2611ba75c23
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545694"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSdistributiondbs** contém uma linha para cada banco de dados de distribuição definido no distribuidor local. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do banco de dados de distribuição.|  
|**min_distretention**|**int**|O período mínimo de retenção, em horas, antes que as transações sejam excluídas.|  
|**max_distretention**|**int**|O período máximo de retenção, em horas, antes que as transações sejam excluídas.|  
|**history_retention**|**int**|O número de horas para retenção do histórico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
