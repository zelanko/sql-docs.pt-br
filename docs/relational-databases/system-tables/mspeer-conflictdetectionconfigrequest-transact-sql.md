---
title: MSpeer_conflictdetectionconfigrequest (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7162681cd957f40a5da0e609124dc3c80624700d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado em replicação ponto a ponto para controlar solicitações de toda a topologia para uma publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifica uma solicitação de configuração de conflito. A coluna request_id em [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) usa esse valor.|  
|publication|**sysname**|Nome da publicação da qual a solicitação de configuração de conflito originou.|  
|sent_date|**datetime**|Data e hora em que a solicitação de configuração de conflito foi iniciada.|  
|tempo limite|**int**|Quantidade de tempo que um procedimento deve esperar por todos os pontos retornarem informações sobre conflitos.|  
|modified_date|**datetime**|Data e hora em que uma fase foi concluída.|  
|progress_phase|**nvarchar (32)**|Identifica a fase atual de processamento, usando um dos seguintes valores:<br /><br /> Started (iniciado)<br /><br /> Explorando topologia<br /><br /> Coletando status<br /><br /> Status coletado|  
|phase_timed_out|**bit**|Indica se a fase atual atingiu o tempo limite.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
