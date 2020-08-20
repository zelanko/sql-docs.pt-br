---
description: MSpeer_request (Transact-SQL)
title: MSpeer_request (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_request
- MSpeer_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_request system table
ms.assetid: ed048c46-7a2f-4ad0-bc7c-c2d65e83b4fb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 19a39eeddd6a528f99e8e111d69a5f2fc6ec1b06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488720"
---
# <a name="mspeer_request-transact-sql"></a>MSpeer_request (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela MSpeer_request é usada em replicação ponto a ponto para controlar solicitações de status para uma determinada publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifica uma solicitação.|  
|publication|**sysname**|Nome da publicação para a qual a solicitação de status foi iniciada.|  
|sent_date|**datetime**|Data e hora em que a solicitação de status foi iniciada.|  
|descrição|**nvarchar(4000)**|Informações definidas pelo usuário que podem ser usadas para identificar solicitações de status individuais.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
