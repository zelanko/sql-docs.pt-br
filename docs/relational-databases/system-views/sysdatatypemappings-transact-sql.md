---
description: sysdatatypemappings (Transact-SQL)
title: sysdatatypemappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad4a6df1ae2dbdd418e133053330095a389bdf24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427528"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição **sysdatatypemappings** é usada para mostrar o mapeamento entre SQL Server tipos de dados e os tipos de dados de um sistema de gerenciamento de banco (DBMS) não SQL Server. Essa exibição é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|A ID do mapeamento de tipo de dados.|  
|**source_dbms**|**sysname**|Indica o nome do DBMS do qual os tipos de dados são mapeados, e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = a origem é um banco de dados SQL Server.<br /><br /> **Oracle** = a origem é um banco de dados Oracle.|  
|**source_version**|**sysname**|Indica a versão do produto do DBMS de origem.|  
|**source_type**|**sysname**|Indica o tipo de dados listado no DBMS de origem.|  
|**source_length_min**|**bigint**|O comprimento mínimo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**source_length_max**|**bigint**|O comprimento máximo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**source_precision_min**|**bigint**|A precisão mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**source_precision_max**|**bigint**|A precisão máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**source_scale_min**|**int**|A escala mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**source_scale_max**|**int**|A escala máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**source_nullable**|**bit**|Indicado se o tipo de dados de destino oferecer suporte a valores nulos.|  
|**source_createparams**|**int**|Somente para uso interno.|  
|**destination_dbms**|**sysname**|Indica o nome do DBMS de destino e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = o destino é um banco de dados SQL Server.<br /><br /> **Oracle** = o destino é um banco de dados Oracle.<br /><br /> **DB2** = o destino é um banco de dados IBM DB2.<br /><br /> **Sybase** = o destino é um banco de dados Sybase.|  
|**destination_version**|**sysname**|A versão de produto do DBMS de destino.|  
|**destination_type**|**sysname**|O tipo de dados no DBMS de destino.|  
|**destination_length**|**bigint**|O comprimento do tipo de dados no DBMS de destino.|  
|**destination_precision**|**bigint**|A precisão do tipo de dados no DBMS de destino.|  
|**destination_scale**|**int**|A escala do tipo de dados no DBMS de destino.|  
|**destination_nullable**|**bit**|Indica se o tipo de dados no DBMS de destino oferece suporte a um valor nulo.|  
|**destination_createparams**|**int**|Somente para uso interno.|  
|**perda**|**bit**|Indica se ocorre perda de dados ao mapear entre o tipo de dados no DBMS de origem e destino.|  
|**is_default**|**bit**|Indica se o mapeamento de tipo de dados é usado por padrão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdatatypemap ](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
