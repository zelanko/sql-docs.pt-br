---
title: MSpub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcf00bab09fb47969439740d4b93b40fd89bf42e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpub_identity_range** tabela oferece suporte ao gerenciamento de intervalo de identidade. Essa tabela é armazenada no banco de dados de assinatura e publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**ObjID**|**int**|A ID da tabela que tem a coluna de identidade administrada pela replicação.|  
|**intervalo**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos à assinatura em um ajuste.|  
|**pub_range**|**bigint**|Controla o tamanho do intervalo dos valores de identidade consecutivos que seriam atribuídos à publicação em um ajuste.|  
|**current_pub_range**|**bigint**|O intervalo atual usado pela publicação. Pode ser diferente de *pub_range* se exibido depois de alterado por **sp_changearticle** e antes do próximo ajuste de intervalo.|  
|**limite**|**int**|Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Quando a porcentagem de valores especificada em *limite* é usado, o agente de distribuição cria um novo intervalo de identidade.|  
|**last_seed**|**bigint**|A associação mais baixa do intervalo atual.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
