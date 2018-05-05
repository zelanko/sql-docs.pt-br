---
title: MStracer_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4f0c3311f7927d15ccdb24be254c893127e5997d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MStracer_history** tabela mantém um registro de todos os tokens de rastreamento que foram recebidas no assinante. Essa tabela é armazenada no banco de dados de distribuição e é usada pela replicação para monitorar o desempenho.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**Int**|Identifica com exclusividade um token de rastreamento.|  
|**agent_id**|**Int**|Identifica o agente que tratou o registro de token de rastreamento.|  
|**subscriber_commit**|**datetime**|A data e hora em que o registro de token de rastreamento foi confirmado no Assinante.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
