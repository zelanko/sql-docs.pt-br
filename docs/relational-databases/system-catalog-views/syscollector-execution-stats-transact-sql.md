---
title: syscollector_execution_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e04c57081f19358786dcc723f6ef2f79757fae2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorexecutionstats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre a execução da tarefa de um pacote ou conjunto de coletas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|Identifica cada execução do conjunto de coleta. Usado para unir essa exibição a outros logs detalhados. Não permite valor nulo.|  
|**task_name**|**nvarchar(128)**|O nome da tarefa do pacote ou conjunto de coletas a que estas informações se destinam. Não permite valor nulo.|  
|**execution_row_count_in**|**Int**|Número de linhas processadas no início do fluxo de dados. Permite valor nulo.|  
|**execution_row_count_out**|**Int**|Número de linhas processadas no final do fluxo de dados. Permite valor nulo.|  
|**execution_row_count_errors**|**Int**|Número de linhas que falharam durante o fluxo de dados. Permite valor nulo.|  
|**execution_time_ms**|**Int**|O tempo, em milissegundos, necessário para a conclusão da tarefa. Permite valor nulo.|  
|**log_time**|**datetime**|A hora em que estas informações foram registradas. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
