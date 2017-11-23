---
title: MSpeer_topologyresponse (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 059fa8cb441bde356e2020a7bf6ffa11e3417ad3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Usado em replicação ponto a ponto para armazenar a resposta de cada nó em uma solicitação de status de topologia. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica uma entrada de solicitação de status de topologia no [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabela.|  
|peer|**sysname**|O nome do instância do servidor que gerou a resposta.|  
|peer_version|**int**|Identifica o número da versão do Publicador.|  
|peer_db|**sysname**|Banco de dados de assinatura no nível que gerou a resposta.|  
|originator_id|**int**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Período de tempo, em dias, que os metadados são armazenados em tabelas de conflitos.|  
|received_date|**datetime**|Hora na qual a solicitação de topologia foi recebida.|  
|connection_info|**xml**|Informações sobre o nó que respondeu à solicitação.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
