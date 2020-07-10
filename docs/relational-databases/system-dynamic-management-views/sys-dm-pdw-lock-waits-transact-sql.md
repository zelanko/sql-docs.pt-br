---
title: sys. dm_pdw_lock_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 14ce0e2aa5b99878ccf9a704defe6ed305ec04a2
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197060"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>sys. dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre as solicitações que estão aguardando bloqueios.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posição da solicitação na lista de espera.|ordinal baseado em 0. Isso não é exclusivo em todas as entradas de espera.|  
|session_id|**nvarchar(32)**|ID da sessão na qual o estado de espera ocorreu.|Consulte session_id em [Sys. dm_pdw_exec_sessions &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|tipo|**nvarchar (255)**|Tipo de espera que essa entrada representa.|Valores possíveis:<br /><br /> Compartilhada<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> Exclusivo|  
|object_type|**nvarchar (255)**|Tipo de objeto que é afetado pela espera.|Valores possíveis:<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar (386)**|Nome ou GUID do objeto especificado que foi afetado pela espera.|Tabelas e exibições são exibidas com nomes de três partes.<br /><br /> Os índices e as estatísticas são exibidos com nomes de quatro partes.<br /><br /> Nomes, entidades de segurança e bancos de dados são nomes de cadeia de caracteres.|  
|request_id|**nvarchar(32)**|ID da solicitação na qual o estado de espera ocorreu.|ID da solicitação.<br /><br /> Este é um GUID para solicitações de carregamento.|  
|request_time|**datetime**|Hora em que o bloqueio ou o recurso foi solicitado.||  
|acquire_time|**datetime**|Hora em que o bloqueio ou o recurso foi adquirido.||  
|state|**nvarchar(50)**|Estado do estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridade do item em espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
