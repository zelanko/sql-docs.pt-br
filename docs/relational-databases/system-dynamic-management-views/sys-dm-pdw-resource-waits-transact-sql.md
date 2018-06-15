---
title: sys.dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4930ac03a9262e73f382ca250fd6d63c233e83b6
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466362"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Exibe informações para todos os tipos de recurso de espera [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posição da solicitação na lista de espera.|ordinal com base em 0. Isso não é exclusivo em todas as entradas de espera.|  
|session_id|**nvarchar(32)**|ID da sessão na qual ocorreu o estado de espera.|Consulte session_id [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Tipo|**nvarchar(255)**|Tipo de espera que representa esta entrada.|Valores possíveis:<br /><br /> Conexão<br /><br /> Simultaneidade de consultas de local<br /><br /> Simultaneidade de consultas distribuídas<br /><br /> Simultaneidade DMS<br /><br /> Simultaneidade de backup|  
|object_type|**nvarchar(255)**|Tipo de objeto que é afetado por espera.|Valores possíveis:<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **APLICATIVO**|  
|object_name|**nvarchar(386)**|Nome ou o GUID do objeto especificado que foi afetado por espera.|Tabelas e exibições são exibidas com nomes de três partes.<br /><br /> Índices e estatísticas são exibidas com nomes de quatro partes.<br /><br /> Nomes de entidades e bancos de dados são nomes de cadeia de caracteres.|  
|request_id|**nvarchar(32)**|ID da solicitação na qual ocorreu o estado de espera.|Identificador QID da solicitação.<br /><br /> Identificador GUID para solicitações de carga.|  
|request_time|**datetime**|Hora em que o bloqueio ou o recurso solicitado.||  
|acquire_time|**datetime**|Hora em que foi adquirido o bloqueio ou recurso.||  
|state|**nvarchar(50)**|Estado do estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**Int**|Prioridade do item de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**Int**|Número de slots de simultaneidade (no máximo 32) reservado para esta solicitação.|1 – para SmallRC<br /><br /> 3 – para MediumRC<br /><br /> 7 para LargeRC<br /><br /> 22 – para XLargeRC|  
|resource_class|**nvarchar(20)**|A classe de recurso para esta solicitação.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
