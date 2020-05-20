---
title: MSsub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsub_identity_range_TSQL
- MSsub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSsub_identity_range system table
ms.assetid: 26e20d28-14ed-44fc-af3b-4de386de4bb8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 965d8530b38aad7d01d9735e603eb3c3a7be0876
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820981"
---
# <a name="mssub_identity_range-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSsub_identity_range** fornece suporte ao gerenciamento de intervalo de identidade para assinaturas. Essa tabela é armazenada nos bancos de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|A ID da tabela que tem a coluna de identidade administrada pela replicação.|  
|**amplitude**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos ao Assinante em um ajuste.|  
|**last_seed**|**bigint**|A associação mais baixa do intervalo atual.|  
|**os**|**int**|Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Quando a porcentagem de valores especificados no *limite* é usada, o agente de distribuição cria um novo intervalo de identidade.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
