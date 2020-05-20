---
title: MSrepl_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c1949134790942ea510060534a4760e76b63469d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824821"
---
# <a name="msrepl_identity_range-transact-sql"></a>MSrepl_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSrepl_identity_range** fornece suporte ao gerenciamento de intervalo de identidade. Essa tabela é armazenada na publicação, nos bancos de dados de assinatura e distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**TableName**|**sysname**|O nome da tabela.|  
|**identity_support**|**int**|Especifica se o tratamento de intervalo de identidade automático está habilitado. 0 especifica que o tratamento de intervalo de identidade automático não está habilitado.|  
|**next_seed**|**bigint**|Se o intervalo de identidade automático estiver habilitado, indicará o ponto de início do próximo intervalo.|  
|**pub_range**|**bigint**|O tamanho do intervalo de identidade do publicador.|  
|**amplitude**|**bigint**|O tamanho dos valores de identidade consecutivos que seria atribuído a assinantes em um ajuste.|  
|**max_identity**|**bigint**|O limite máximo do intervalo de identidade.|  
|**os**|**int**|A porcentagem de limite do intervalo de identidade.|  
|**current_max**|**bigint**|O máximo atual que pode ser atribuído, mas que não será necessariamente atribuído.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
