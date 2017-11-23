---
title: sys.dm_exec_valid_use_hints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
caps.latest.revision: "5"
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61efec0bec550e68ce19e1285c381c0649849450
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecvalidusehints-transact-sql"></a>sys.dm_exec_valid_use_hints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna [dica USE](../../t-sql/queries/hints-transact-sql-query.md) suporte para nomes de dica. Ele lista o nome de uma dica por linha.  
  
Use essa DMV para ver a lista de todas as dicas com suporte em notação de dica de uso.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|O nome da dica.|

Consulte [dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md) para obter descrições de cada dica.

Introduzido no [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1.
  
## <a name="see-also"></a>Consulte também  
    
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

