---
description: sys.dm_pdw_wait_stats (Transact-SQL)
title: sys.dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 417b5f5d88d5a150653e6910eabb8f7692657b2c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461567"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações relacionadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estado do sistema operacional relacionadas a instâncias em execução em nós diferentes. Para obter uma lista de tipos de espera e sua descrição, consulte [Sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx).  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|ID do nó ao qual essa entrada se refere.||  
|**wait_name**|**nvarchar(255)**|Nome do tipo de espera.||  
|**max_wait_time**|**bigint**|Tempo de espera máximo deste tipo de espera.||  
|**request_count**|**bigint**|Número de esperas desse tipo de espera pendentes.||  
|**signal_time**|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.||  
|**completed_count**|**bigint**|Número total de esperas desse tipo concluídas desde a última reinicialização do servidor.||  
|**wait_time**|**bigint**|Tempo de espera total para esse tipo de espera em millisecons. Inclusive signal_time.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [&#41;&#40;Transact-SQL de sys.dm_pdw_waits ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
