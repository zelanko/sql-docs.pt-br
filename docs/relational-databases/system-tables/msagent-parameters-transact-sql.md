---
description: MSagent_parameters (Transact-SQL)
title: MSagent_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_parameters_TSQL
- MSagent_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_parameters system table
ms.assetid: be30abc9-c00d-446f-b1b4-1269772f37e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f462e59611b33d35762ad0941e871c196990f2c5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544513"
---
# <a name="msagent_parameters-transact-sql"></a>MSagent_parameters (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSagent_parameters** contém parâmetros associados a um perfil de agente. Os nomes de parâmetro são os mesmos que os suportados pelo agente. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|A ID do perfil da tabela de **MSagent_profiles** .|  
|**parameter_name**|**sysname**|O nome do parâmetro.|  
|**value**|**nvarchar(255)**|O valor do parâmetro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
