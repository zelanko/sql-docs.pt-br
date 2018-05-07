---
title: sysdatatypemappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a447bf38ce77889b2dc6e0e0888b7f4cccb93c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **sysdatatypemappings** exibição é usada para mostrar o mapeamento entre tipos de dados do SQL Server e tipos de dados de um sistema de gerenciamento de banco de dados do SQL Server (DBMS). Essa exibição é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**Int**|A ID do mapeamento de tipo de dados.|  
|**source_dbms**|**sysname**|Indica o nome do DBMS do qual os tipos de dados são mapeados, e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = a origem é um banco de dados do SQL Server.<br /><br /> **ORACLE** = a origem é um banco de dados Oracle.|  
|**source_version**|**sysname**|Indica a versão do produto do DBMS de origem.|  
|**source_type**|**sysname**|Indica o tipo de dados listado no DBMS de origem.|  
|**source_length_min**|**bigint**|O comprimento mínimo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**source_length_max**|**bigint**|O comprimento máximo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**source_precision_min**|**bigint**|A precisão mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**source_precision_max**|**bigint**|A precisão máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**source_scale_min**|**Int**|A escala mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**source_scale_max**|**Int**|A escala máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**source_nullable**|**bit**|Indicado se o tipo de dados de destino oferecer suporte a valores nulos.|  
|**source_createparams**|**Int**|Somente para uso interno.|  
|**destination_dbms**|**sysname**|Indica o nome do DBMS de destino e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = o destino é um banco de dados do SQL Server.<br /><br /> **ORACLE** = o destino é um banco de dados Oracle.<br /><br /> **DB2** = o destino é um banco de dados IBM DB2.<br /><br /> **SYBASE** = o destino é um banco de dados Sybase.|  
|**destination_version**|**sysname**|A versão de produto do DBMS de destino.|  
|**destination_type**|**sysname**|O tipo de dados no DBMS de destino.|  
|**destination_length**|**bigint**|O comprimento do tipo de dados no DBMS de destino.|  
|**destination_precision**|**bigint**|A precisão do tipo de dados no DBMS de destino.|  
|**destination_scale**|**Int**|A escala do tipo de dados no DBMS de destino.|  
|**destination_nullable**|**bit**|Indica se o tipo de dados no DBMS de destino oferece suporte a um valor nulo.|  
|**destination_createparams**|**Int**|Somente para uso interno.|  
|**perda**|**bit**|Indica se ocorre perda de dados ao mapear entre o tipo de dados no DBMS de origem e destino.|  
|**is_default**|**bit**|Indica se o mapeamento de tipo de dados é usado por padrão.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
