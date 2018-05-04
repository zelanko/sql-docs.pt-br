---
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 78ef5ef914c308d86e2fa7b78ca302705482d28e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre operações de carregamento em andamento e concluídas em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. As informações persistem entre os reinícios do sistema.  
  
|||||  
|-|-|-|-|  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|run_id|**Int**|Identificador exclusivo de um carregador de executar.||  
|Estágio|**nvarchar(30)**|O estágio atual para a execução.|'CREATE_STAGING', 'DMS_LOAD', 'LOAD_INSERT', 'LOAD_CLEANUP'|  
|request_id|**nvarchar(32)**|ID da solicitação em execução neste estágio.||  
|status|**nvarchar(16)**|Status desta fase.||  
|start_time|**datetime**|Hora em que o estágio foi iniciado.||  
|end_time|**datetime**|Hora em que o estágio terminou, se houver.|NULL se não iniciado ou estiver em andamento.|  
|total_elapsed_time|**Int**|Tempo total neste estágio gasto (ou, gasto até o momento) em execução.|Se total_elapsed_time excede o valor máximo para um inteiro (24.8 dias em milissegundos), isso causará falha materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
