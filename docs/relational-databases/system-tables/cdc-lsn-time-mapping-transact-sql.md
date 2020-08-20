---
description: cdc.lsn_time_mapping (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a716c51821c3efccd0bdebea3f28f9376d29b7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488925"
---
# <a name="cdclsn_time_mapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada transação que tem linhas em uma tabela de alteração. Esta tabela é usada para mapear entre os valores confirmados de LSN (número de sequência de log) e a hora em que a transação foi confirmada. Também podem ser registradas entradas, para as quais não há entradas de tabelas de alteração. Isso permite a tabela registrar a conclusão de LSN processado em períodos de baixa ou nenhuma atividade de alteração.  
  
 É recomendável não consultar diretamente as tabelas do sistema. Em vez disso, execute as funções de sistema [fn_cdc_map_lsn_to_time &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) e [sys. Fn_cdc_map_time_to_lsn &#40;o transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) .  
    
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|LSN da transação confirmada.|  
|**tran_begin_time**|**datetime**|Hora em que a transação associada com o LSN começou.|  
|**tran_end_time**|**datetime**|Hora em que a transação terminou.|  
|**tran_id**|**varbinary (10)**|ID da transação.|  
  
## <a name="see-also"></a>Consulte Também  
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [cdc.&#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
