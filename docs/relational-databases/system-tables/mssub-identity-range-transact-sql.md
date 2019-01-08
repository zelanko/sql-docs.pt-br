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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a300f4be77bf6e63722f41553f0cb998cb48827
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750458"
---
# <a name="mssubidentityrange-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsub_identity_range** tabela oferece suporte ao gerenciamento de intervalo de identidade para assinaturas. Essa tabela é armazenada nos bancos de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|A ID da tabela que tem a coluna de identidade administrada pela replicação.|  
|**range**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos ao Assinante em um ajuste.|  
|**last_seed**|**bigint**|A associação mais baixa do intervalo atual.|  
|**threshold**|**int**|Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Quando a porcentagem de valores especificada em *limite* é usado, o agente de distribuição cria um novo intervalo de identidade.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
