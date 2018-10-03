---
title: CDC. lsn_time_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3118a814d18013a4360dd9afdcd1e09dcc483545
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822044"
---
# <a name="cdclsntimemapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada transação que tem linhas em uma tabela de alteração. Esta tabela é usada para mapear entre os valores confirmados de LSN (número de sequência de log) e a hora em que a transação foi confirmada. Também podem ser registradas entradas, para as quais não há entradas de tabelas de alteração. Isso permite a tabela registrar a conclusão de LSN processado em períodos de baixa ou nenhuma atividade de alteração.  
  
 É recomendável não consultar diretamente as tabelas do sistema. Em vez disso, execute as [fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) e [fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) funções do sistema.  
    
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|LSN da transação confirmada.|  
|**tran_begin_time**|**datetime**|Hora em que a transação associada com o LSN começou.|  
|**tran_end_time**|**datetime**|Hora em que a transação terminou.|  
|**tran_id**|**varbinary(10)**|ID da transação.|  
  
## <a name="see-also"></a>Consulte também  
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [CDC. &#60;capture_instance&#62;CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
