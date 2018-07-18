---
title: sys.dm_exec_distributed_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d61b26c1af6a588140cdf47308ee8f69ecd42b2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982538"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as solicitações ativas no momento ou recentemente em consultas do PolyBase. Ele lista uma linha por solicitação/consulta.  
  
 Com base em sessão e solicitação de identificação, um usuário pode recuperar as solicitações distribuídas reais geradas para ser executada – por meio do sys.dm_exec_distributed_requests. Por exemplo, uma consulta que envolva SQL regular e as tabelas externas de SQL será ser decomposta em várias instruções/solicitações executadas em vários nós de computação. Para acompanhar as etapas distribuídas entre todos os nós de computação, apresentamos uma ID de execução 'global' que pode ser usada para acompanhar todas as operações em nós de computação associados com uma solicitação específica e o operador, respectivamente.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|A chave para este modo de exibição. Id numérico exclusivo associado com a solicitação.|Exclusivo entre todas as solicitações no sistema.|  
|execution_id|**nvarchar(32**|Id numérico exclusivo associado à sessão em que essa consulta foi executada.||  
|status|**nvarchar(32**|Status atual da solicitação.|'Pending', 'Authorizing', 'AcquireSystemResources', 'Initializing', 'Plan', 'Parsing', 'AquireResources', 'Running', 'Cancelling', 'Complete', 'Failed', 'Cancelled'.|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado à solicitação, se houver.|Definido como NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora em que a execução da solicitação foi iniciada.|0 para solicitações em fila; Caso contrário, válido datetime menor ou igual à hora atual.|  
|end_time|**datetime**|Hora em que o mecanismo concluiu a solicitação de compilação.|NULL para solicitações em fila ou do Active Directory; Caso contrário, um datetime válido menor ou igual à hora atual.|  
|total_elapsed_time|**int**|Tempo decorrido na execução desde que a solicitação foi iniciada, em milissegundos.|Entre 0 e a diferença entre start_time e end_time. Se total_elapsed_time exceder o valor máximo para um número inteiro, o total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido." O valor máximo em milissegundos é equivalente a 24,8 dias.|  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
