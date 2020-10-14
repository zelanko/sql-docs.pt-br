---
description: sys.pdw_loader_run_stages (Transact-SQL)
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 288810d6143bcdb98e7bf3257f5958b2cf5f91ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036729"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contém informações sobre as operações de carregamento em andamento e concluídas no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . As informações persistem entre os reinícios do sistema.  
  
| Nome da coluna | Tipo de Dados | DESCRIÇÃO | Intervalo |
| ----------- | --------- | ----------- | ----- |
|run_id|**int**|Identificador exclusivo de uma execução de carregador.||  
|preparar|**nvarchar(30)**|O estágio atual para a execução.|' CREATE_STAGING ', ' DMS_LOAD ', ' LOAD_INSERT ', ' LOAD_CLEANUP '|  
|request_id|**nvarchar(32)**|ID da solicitação que está executando este estágio.||  
|status|**nvarchar (16)**|Status desta fase.||  
|start_time|**datetime**|Hora em que o estágio foi iniciado.||  
|end_time|**datetime**|Hora em que o estágio terminou, se houver.|NULL se não for iniciado ou estiver em andamento.|  
|total_elapsed_time|**int**|Tempo total que esse estágio gastou (ou passou até o momento) em execução.|Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
