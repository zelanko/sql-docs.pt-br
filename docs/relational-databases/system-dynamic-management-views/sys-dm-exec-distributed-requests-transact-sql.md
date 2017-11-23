---
title: sys.dm_exec_distributed_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 39b16d051c3300599a220f4f2ce21904db208571
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as solicitações ativas no momento ou recentemente em consultas do PolyBase. Ele lista uma linha por solicitar de consulta.  
  
 Com base em sessão e solicitação de identificação, um usuário pode recuperar as solicitações distribuídas reais geradas para ser executado – via sys.dm_exec_distributed_requests. Por exemplo, uma consulta que envolva SQL regular e tabelas SQL externas será ser decomposta em várias instruções/solicitações executadas em vários nós de computação. Para controlar as etapas distribuídas em todos os nós de computação, apresentamos uma ID de execução 'global' que pode ser usada para rastrear todas as operações em nós de computação associados com uma solicitação específica e o operador, respectivamente.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|Chave para este modo de exibição. Id numérico exclusivo associado à solicitação.|Exclusivo entre todas as solicitações no sistema.|  
|execution_id|**nvarchar (32**|Id numérico exclusivo associado à sessão em que essa consulta foi executada.||  
|status|**nvarchar (32**|Status atual da solicitação.|'Pendente', 'Autorizar', 'AcquireSystemResources', 'Inicializando', 'Plano', 'Analisar', 'AquireResources', 'Em execução', 'Cancelar', 'Concluir', 'com falha', 'Cancelado'.|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado à solicitação, se houver.|Definido como NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora em que a execução da solicitação foi iniciada.|0 para solicitações em fila; Caso contrário, válido datetime menor ou igual à hora atual.|  
|end_time|**datetime**|Hora em que o mecanismo concluiu compilar a solicitação.|NULL para solicitações em fila ou ativas; Caso contrário, um datetime válido menor ou igual à hora atual.|  
|total_elapsed_time|**int**|Tempo decorrido na execução desde que a solicitação foi iniciada, em milissegundos.|Entre 0 e a diferença entre start_time e end_time. Se total_elapsed_time excede o valor máximo para um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido." O valor máximo em milissegundos é equivalente a 24.8 dias.|  
  
## <a name="see-also"></a>Consulte também  
 [PolyBase, solucionando problemas com exibições de gerenciamento dinâmico](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
