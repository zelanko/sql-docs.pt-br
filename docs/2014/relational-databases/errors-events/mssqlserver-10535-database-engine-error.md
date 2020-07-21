---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68070291c5e7f50d423b74338dc1f6baeb9c6dfa
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554111"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10535|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_PLAN|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque não foi encontrado no cache de planos um plano que corresponda ao identificador de plano especificado. Especifique um identificador de plano em cache. Para obter uma lista de identificadores de plano em cache, consulte a exibição de gerenciamento dinâmico sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicação  
 Não foi localizado no cache de planos um plano que corresponda ao identificador de plano especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique um identificador de plano em cache. Para obter uma lista de identificadores de plano em cache, consulte a exibição de gerenciamento dinâmico sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_create_plan_guide_from_handle](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
