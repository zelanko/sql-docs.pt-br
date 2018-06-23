---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ff4797fdd9d206ca459bc84facccfc588aafba00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118670"
---
# <a name="mssqlserver10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10535|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_PLAN|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque não foi encontrado no cache de planos um plano que corresponda ao identificador de plano especificado. Especifique um identificador de plano em cache. Para obter uma lista de identificadores de plano em cache, consulte a exibição de gerenciamento dinâmico sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicação  
 Não foi localizado no cache de planos um plano que corresponda ao identificador de plano especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique um identificador de plano em cache. Para obter uma lista de identificadores de plano em cache, consulte a exibição de gerenciamento dinâmico sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
