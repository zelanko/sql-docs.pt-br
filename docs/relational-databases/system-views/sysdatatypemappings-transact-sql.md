---
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
manager: craigg
ms.openlocfilehash: 31f90836b26d9551cc3e5a1200208cc51e3ef30a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756938"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **sysdatatypemappings** exibição é usada para mostrar o mapeamento entre tipos de dados do SQL Server e tipos de dados de um sistema de gerenciamento de banco de dados (DBMS) não SQL Server. Essa exibição é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|A ID do mapeamento de tipo de dados.|  
|**source_dbms**|**sysname**|Indica o nome do DBMS do qual os tipos de dados são mapeados, e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = a origem é um banco de dados do SQL Server.<br /><br /> **ORACLE** = a origem é um banco de dados Oracle.|  
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
|**destination_dbms**|**sysname**|Indica o nome do DBMS de destino e pode ser um dos seguintes valores:<br /><br /> **MSSQLSERVER** = o destino é um banco de dados do SQL Server.<br /><br /> **ORACLE** = o destino é um banco de dados Oracle.<br /><br /> **DB2** = o destino é um banco de dados IBM DB2.<br /><br /> **SYBASE** = o destino é um banco de dados Sybase.|  
|**destination_version**|**sysname**|A versão de produto do DBMS de destino.|  
|**destination_type**|**sysname**|O tipo de dados no DBMS de destino.|  
|**destination_length**|**bigint**|O comprimento do tipo de dados no DBMS de destino.|  
|**destination_precision**|**bigint**|A precisão do tipo de dados no DBMS de destino.|  
|**destination_scale**|**int**|A escala do tipo de dados no DBMS de destino.|  
|**destination_nullable**|**bit**|Indica se o tipo de dados no DBMS de destino oferece suporte a um valor nulo.|  
|**destination_createparams**|**int**|Somente para uso interno.|  
|**perda de dados**|**bit**|Indica se ocorre perda de dados ao mapear entre o tipo de dados no DBMS de origem e destino.|  
|**is_default**|**bit**|Indica se o mapeamento de tipo de dados é usado por padrão.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
