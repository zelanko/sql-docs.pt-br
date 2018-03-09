---
title: MSpeer_response (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ddd727f2278d78888ad9bafce691c17a20eb901
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerresponse-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpeer_response** tabela é usada em replicação ponto a ponto para armazenar a resposta de cada nó a uma solicitação de status de publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|Identifica uma entrada de solicitação de status no [MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) tabela.|  
|**ponto a ponto**|**sysname**|O par que gerou a resposta.|  
|**peer_db**|**sysname**|O banco de dados de assinatura no nível que gerou a resposta.|  
|**received_date**|**datetime**|A data e hora de envio da solicitação de item do mesmo nível.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
