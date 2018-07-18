---
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: 8
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5521b046d49fe27c7dd1a174f960caec54e8626e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969643"
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre operações de carga em andamento e concluídas em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. As informações persistem entre os reinícios do sistema.  
  
|||||  
|-|-|-|-|  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|run_id|**int**|Identificador exclusivo de um carregador de executar.||  
|estágio|**nvarchar(30)**|O estágio atual para a execução.|'CREATE_STAGING', 'DMS_LOAD', 'LOAD_INSERT', 'LOAD_CLEANUP'|  
|request_id|**nvarchar(32)**|ID da solicitação em execução neste estágio.||  
|status|**nvarchar(16)**|Status desta fase.||  
|start_time|**datetime**|Hora em que o estágio foi iniciado.||  
|end_time|**datetime**|Hora em que o estágio terminou, se houver.|NULL se não foi iniciado ou em andamento.|  
|total_elapsed_time|**int**|Tempo total neste estágio gasto (ou até o momento de gasto) em execução.|Se total_elapsed_time exceder o valor máximo para um inteiro (24,8 dias em milissegundos), ela causará falha de materialização devido a estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
