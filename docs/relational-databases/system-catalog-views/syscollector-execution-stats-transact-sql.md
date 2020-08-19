---
description: syscollector_execution_stats (Transact-SQL)
title: syscollector_execution_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ed50c37df682bf3ea41478c29847ca7daba0e448
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490047"
---
# <a name="syscollector_execution_stats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre a execução da tarefa de um pacote ou conjunto de coletas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|Identifica cada execução do conjunto de coleta. Usado para unir essa exibição a outros logs detalhados. Não permite valor nulo.|  
|**task_name**|**nvarchar(128)**|O nome da tarefa do pacote ou conjunto de coletas a que estas informações se destinam. Não permite valor nulo.|  
|**execution_row_count_in**|**int**|Número de linhas processadas no início do fluxo de dados. Permite valor nulo.|  
|**execution_row_count_out**|**int**|Número de linhas processadas no final do fluxo de dados. Permite valor nulo.|  
|**execution_row_count_errors**|**int**|Número de linhas que falharam durante o fluxo de dados. Permite valor nulo.|  
|**execution_time_ms**|**int**|O tempo, em milissegundos, necessário para a conclusão da tarefa. Permite valor nulo.|  
|**log_time**|**datetime**|A hora em que estas informações foram registradas. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do coletor de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
