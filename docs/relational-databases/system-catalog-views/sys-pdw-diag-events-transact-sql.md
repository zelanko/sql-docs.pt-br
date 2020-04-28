---
title: sys. pdw_diag_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 59bb3e9c-2829-49a0-b382-652ed1f54f88
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4aa83c4931e1cce4b4b813baa489ae43798db594
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127559"
---
# <a name="syspdw_diag_events-transact-sql"></a>sys. pdw_diag_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre eventos que podem ser incluídos em sessões de diagnóstico no sistema.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar (255)**|Nome do evento de diagnóstico específico.||  
|**original**|**nvarchar (255)**|Origem do evento (mecanismo, geral, DMS, etc.)||  
|**is_enabled**|**bit**|Se o evento está sendo publicado.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
