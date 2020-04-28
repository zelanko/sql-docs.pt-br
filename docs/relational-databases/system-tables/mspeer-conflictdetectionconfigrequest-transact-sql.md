---
title: MSpeer_conflictdetectionconfigrequest (T-SQL)
description: Descreve o MSPeer_conflictdetectionconfigurerequest procedimento armazenado usado para rastrear solicitações de configuração em toda a topologia para uma publicação ponto a ponto.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 090236bd5e0bd0429985ff9c54039a576950ec84
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75322089"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado em replicação ponto a ponto para controlar solicitações de toda a topologia para uma publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifica uma solicitação de configuração de conflito. A coluna request_id em [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) usa esse valor.|  
|publication|**sysname**|Nome da publicação da qual a solicitação de configuração de conflito originou.|  
|sent_date|**datetime**|Data e hora em que a solicitação de configuração de conflito foi iniciada.|  
|tempo limite|**int**|Quantidade de tempo que um procedimento deve esperar por todos os pontos retornarem informações sobre conflitos.|  
|modified_date|**datetime**|Data e hora em que uma fase foi concluída.|  
|progress_phase|**nvarchar(32)**|Identifica a fase atual de processamento, usando um dos seguintes valores:<br /><br /> Started (iniciado)<br /><br /> Explorando topologia<br /><br /> Coletando status<br /><br /> Status coletado|  
|phase_timed_out|**bit**|Indica se a fase atual atingiu o tempo limite.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
