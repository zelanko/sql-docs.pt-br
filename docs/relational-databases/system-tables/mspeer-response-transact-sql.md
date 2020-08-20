---
description: MSpeer_response (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0bb95540f6731c9fc1d49711b85d03c9fa2efad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488690"
---
# <a name="mspeer_response-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSpeer_response** é usada na replicação ponto a ponto para armazenar a resposta de cada nó a uma solicitação de status de publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|Identifica uma entrada de solicitação de status na tabela [MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) .|  
|**pares**|**sysname**|O par que gerou a resposta.|  
|**peer_db**|**sysname**|O banco de dados de assinatura no nível que gerou a resposta.|  
|**received_date**|**datetime**|A data e hora de envio da solicitação de item do mesmo nível.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
