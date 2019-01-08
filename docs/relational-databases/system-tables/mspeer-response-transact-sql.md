---
title: MSpeer_response (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adbddf6f26c28c5fba396b00892b97d828e60222
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757988"
---
# <a name="mspeerresponse-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpeer_response** tabela é usada na replicação ponto a ponto para armazenar a resposta de cada nó a uma solicitação de status de publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|Identifica uma entrada de solicitação de status na [MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) tabela.|  
|**ponto a ponto**|**sysname**|O par que gerou a resposta.|  
|**peer_db**|**sysname**|O banco de dados de assinatura no nível que gerou a resposta.|  
|**received_date**|**datetime**|A data e hora de envio da solicitação de item do mesmo nível.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
