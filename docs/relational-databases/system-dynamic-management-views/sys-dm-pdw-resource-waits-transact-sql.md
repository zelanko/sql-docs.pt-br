---
title: sys.dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 704fcdc72f571485f10b76860a632c61233ed296
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000848"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Exibe espera informações para todos os tipos de recurso em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posição da solicitação na lista de espera.|ordinal com base em 0. Ele não é exclusivo em todas as entradas de espera.|  
|session_id|**nvarchar(32)**|ID da sessão na qual ocorreu o estado de espera.|Consulte session_id [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Tipo|**nvarchar(255)**|Tipo de espera que essa entrada representa.|Valores possíveis:<br /><br /> Conexão<br /><br /> Simultaneidade de consultas locais<br /><br /> Simultaneidade de consultas distribuídas<br /><br /> Simultaneidade do DMS<br /><br /> Simultaneidade de backup|  
|object_type|**nvarchar(255)**|Tipo de objeto que é afetado pelo tempo de espera.|Valores possíveis:<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **APLICATIVO**|  
|object_name|**nvarchar(386)**|Nome ou GUID do objeto especificado que foi afetado por tempo de espera.|Tabelas e exibições são exibidas com nomes de três partes.<br /><br /> Índices e estatísticas são exibidas com nomes de quatro partes.<br /><br /> Nomes de entidades de segurança e bancos de dados são nomes de cadeia de caracteres.|  
|request_id|**nvarchar(32)**|ID da solicitação em que ocorreu o estado de espera.|Identificador QID da solicitação.<br /><br /> Identificador GUID para solicitações de carga.|  
|request_time|**datetime**|Hora em que o bloqueio ou o recurso foi solicitado.||  
|acquire_time|**datetime**|Hora em que foi adquirido o bloqueio ou recurso.||  
|state|**nvarchar(50)**|Estado do estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridade do item de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Número de slots de simultaneidade (no máximo 32) reservado para esta solicitação.|1 – para SmallRC<br /><br /> 3 – para MediumRC<br /><br /> 7 para LargeRC<br /><br /> 22 – para XLargeRC|  
|resource_class|**nvarchar(20)**|A classe de recurso para esta solicitação.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
