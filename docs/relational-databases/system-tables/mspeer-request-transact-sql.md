---
title: MSpeer_request (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MSpeer_request
- MSpeer_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_request system table
ms.assetid: ed048c46-7a2f-4ad0-bc7c-c2d65e83b4fb
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1628130479e9fe2bc784caac37c2ae68f07d8c2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mspeerrequest-transact-sql"></a>MSpeer_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela MSpeer_request é usada em replicação ponto a ponto para controlar solicitações de status para uma determinada publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|id|**Int**|Identifica uma solicitação.|  
|publication|**sysname**|Nome da publicação para a qual a solicitação de status foi iniciada.|  
|sent_date|**datetime**|Data e hora em que a solicitação de status foi iniciada.|  
|descrição|**nvarchar(4000)**|Informações definidas pelo usuário que podem ser usadas para identificar solicitações de status individuais.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
